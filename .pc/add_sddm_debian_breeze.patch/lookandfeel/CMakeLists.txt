plasma_install_package(org.lingmo.ocean org.lingmo.ocean.desktop look-and-feel lookandfeel)
plasma_install_package(org.lingmo.oceandark org.lingmo.oceandark.desktop look-and-feel lookandfeel)

if (INSTALL_SDDM_THEME)
    configure_file(sddm-theme/theme.conf.cmake ${CMAKE_CURRENT_BINARY_DIR}/sddm-theme/theme.conf)

# Install the login theme into the SDDM directory
# Longer term we need to look at making SDDM load from look and feel somehow.. and allow copying at runtime
    #NOTE this trailing slash is important to rename the directory
    install(DIRECTORY sddm-theme/ DESTINATION ${KDE_INSTALL_FULL_DATADIR}/sddm/themes/breeze PATTERN "README.txt" EXCLUDE PATTERN "components" EXCLUDE PATTERN "dummydata" EXCLUDE
    PATTERN "theme.conf.cmake" EXCLUDE)
    install(FILES ${CMAKE_CURRENT_BINARY_DIR}/sddm-theme/theme.conf DESTINATION ${KDE_INSTALL_FULL_DATADIR}/sddm/themes/breeze)
    install(DIRECTORY org.lingmo.ocean/contents/components DESTINATION ${KDE_INSTALL_FULL_DATADIR}/sddm/themes/breeze PATTERN "README.txt" EXCLUDE)
endif()

if (BUILD_TESTING)
    add_subdirectory(autotests/lockscreen)
endif()
