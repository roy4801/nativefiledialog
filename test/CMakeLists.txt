cmake_minimum_required(VERSION 3.10)

project(nfd-tests)
# Add test_opendialog
add_executable(test_opendialog
    test_opendialog.c
)
target_link_libraries(test_opendialog nfd::nfd)
# Add test_opendialogmultiple
add_executable(test_opendialogmultiple
    test_opendialogmultiple.c
)
target_link_libraries(test_opendialogmultiple nfd::nfd)
# Add test_pickfolder
add_executable(test_pickfolder
    test_pickfolder.c
)
target_link_libraries(test_pickfolder nfd::nfd)
# Add test_savedialog
add_executable(test_savedialog
    test_savedialog.c
)
target_link_libraries(test_savedialog nfd::nfd)