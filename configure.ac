
# Initialize Autoconf
AC_PREREQ([2.70])
AC_INIT([libXext], [1.3.6],
        [https://gitlab.freedesktop.org/xorg/lib/libxext/-/issues], [libXext])
AC_CONFIG_SRCDIR([Makefile.am])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIR([m4])

# Set common system defines for POSIX extensions, such as _GNU_SOURCE
# Must be called before any macros that run the compiler (like LT_INIT)
# to avoid autoconf errors.
AC_USE_SYSTEM_EXTENSIONS

# Initialize Automake
AM_INIT_AUTOMAKE([foreign dist-xz])

# Initialize libtool
LT_INIT

# Require xorg-macros minimum of 1.12 for DocBook external references
m4_ifndef([XORG_MACROS_VERSION],
          [m4_fatal([must install xorg-macros 1.12 or later before running autoconf/autogen])])
XORG_MACROS_VERSION(1.12)
XORG_DEFAULT_OPTIONS
XORG_ENABLE_SPECS
XORG_WITH_XMLTO(0.0.22)
XORG_WITH_FOP
XORG_WITH_XSLTPROC
XORG_CHECK_SGML_DOCTOOLS(1.8)
XORG_CHECK_MALLOC_ZERO

# Determine .so library version per platform
# based on SharedXextRev in monolith xc/config/cf/*Lib.tmpl
if test "x$XEXT_SOREV" = "x" ; then
    case $host_os in
	openbsd*)	XEXT_SOREV=8:0 		;;
	solaris*)       XEXT_SOREV=0 		;;
	*)              XEXT_SOREV=6:4:0 	;;
    esac
fi
AC_SUBST(XEXT_SOREV)

# Obtain compiler/linker options for dependencies
PKG_CHECK_MODULES(XEXT, [xproto >= 7.0.13] [x11 >= 1.6] [xextproto >= 7.1.99])

AX_GCC_BUILTIN([__builtin_popcountl])
AC_REPLACE_FUNCS([reallocarray])

# Allow checking code with lint, sparse, etc.
XORG_WITH_LINT
XORG_LINT_LIBRARY([Xext])

AC_CONFIG_FILES([Makefile
		man/Makefile
		src/Makefile
		specs/Makefile
		xext.pc])
AC_OUTPUT
