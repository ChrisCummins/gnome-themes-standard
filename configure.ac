dnl Process this file with autoconf to produce a configure script.
AC_PREREQ(2.53)

AC_INIT([gnome-themes-standard], [3.8.0],
        [http://bugzilla.gnome.org/enter_bug.cgi?product=gnome-themes-standard])

AM_INIT_AUTOMAKE([1.9 tar-ustar foreign dist-xz no-dist-gzip])
m4_ifdef([AM_SILENT_RULES],[AM_SILENT_RULES([yes])])

PKG_PROG_PKG_CONFIG([0.19])

AC_PROG_SED
AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_MAKE_SET
AM_PATH_GLIB_2_0

dnl Initialize libtool
AM_DISABLE_STATIC
AC_LIBTOOL_WIN32_DLL
AM_PROG_LIBTOOL

dnl Initialize intltool
IT_PROG_INTLTOOL([0.40.0])

GETTEXT_PACKAGE="${PACKAGE}"
AC_SUBST(GETTEXT_PACKAGE)

AC_ARG_ENABLE([gtk3-engine],
              AC_HELP_STRING([--disable-gtk3-engine],
                             [Disable Gtk+ 3.x engine [default=no]]),
              enable_gtk3_engine=$enableval,
              enable_gtk3_engine=yes)
AC_MSG_CHECKING([building gtk3 engine])
AM_CONDITIONAL(GTK3_ENGINE, test "x$enable_gtk3_engine" = "xyes")
AC_MSG_RESULT([$enable_gtk3_engine])

GTK_VERSION_REQUIRED=3.6.2
if test "x$enable_gtk3_engine" = "xyes"; then
  PKG_CHECK_MODULES([GTK3_ENGINE], [gtk+-3.0 >= $GTK_VERSION_REQUIRED librsvg-2.0])
  PKG_CHECK_MODULES([HIGHCONTRAST], [cairo gio-2.0 gdk-pixbuf-2.0 gdk-3.0])
fi

GTK3_VERSION=`$PKG_CONFIG --variable=gtk_binary_version gtk+-3.0`
AC_SUBST(GTK3_VERSION)

AC_ARG_ENABLE([gtk2-engine],
              AC_HELP_STRING([--disable-gtk2-engine],
                             [Disable Gtk+-2 engine [default=no]]),
              enable_gtk2_engine=$enableval,
              enable_gtk2_engine=yes)
AC_MSG_CHECKING([building gtk2 engine])
AM_CONDITIONAL(GTK2_ENGINE, test "x$enable_gtk2_engine" = "xyes")
AC_MSG_RESULT([$enable_gtk2_engine])

GTK2_VERSION_REQUIRED=2.24.15
if test "x$enable_gtk2_engine" = "xyes"; then
  PKG_CHECK_MODULES([GTK2_ENGINE], [gtk+-2.0 >= $GTK2_VERSION_REQUIRED gdk-2.0 >= $GTK2_VERSION_REQUIRED])
fi

GTK2_VERSION=`$PKG_CONFIG --variable=gtk_binary_version gtk+-2.0`
AC_SUBST(GTK2_VERSION)

GLIB_COMPILE_RESOURCES=`$PKG_CONFIG --variable glib_compile_resources gio-2.0`
AC_SUBST(GLIB_COMPILE_RESOURCES)

AC_PATH_PROG(GTK_UPDATE_ICON_CACHE, gtk-update-icon-cache)
if test -z "$GTK_UPDATE_ICON_CACHE"; then
    AC_MSG_ERROR([Could not find gtk-update-icon-cache])
fi

# Workaround to make aclocal get the right flags
AC_SUBST(ACLOCAL_AMFLAGS, "\${ACLOCAL_FLAGS}")

AC_CONFIG_FILES([
Makefile
themes/Makefile
themes/Adwaita/Makefile
themes/Adwaita/backgrounds/Makefile
themes/Adwaita/cursors/Makefile
themes/Adwaita/gtk-2.0/Makefile
themes/Adwaita/gtk-3.0/Makefile
themes/Adwaita/metacity-1/Makefile
themes/HighContrast/Makefile
themes/HighContrast/gtk-2.0/Makefile
themes/HighContrast/gtk-3.0/Makefile
themes/HighContrast/icons/Makefile
themes/HighContrast/metacity-1/Makefile
po/Makefile.in
])

AC_OUTPUT
