set(LibraryVersion "fuelet_smart_contract_wallet-v1.8.0") # generated; do not edit

# The Flutter tooling requires that developers have CMake 3.10 or later
# installed. You should not increase this version, as doing so will cause
# the plugin to fail to compile for some customers of the plugin.
cmake_minimum_required(VERSION 3.10)

# Project-level configuration.
set(PROJECT_NAME "flutter_fuelet_smart_contract_wallet")
project(${PROJECT_NAME} LANGUAGES CXX)

# Download the binaries if they are not already present.
set(LibRoot "${CMAKE_CURRENT_SOURCE_DIR}/${LibraryVersion}")
set(ArchivePath "${LibRoot}.tar.gz")
if(NOT EXISTS ${ArchivePath})
  file(DOWNLOAD
    "https://github.com/Fuelet/SmartContractWalletSDK/releases/download/${LibraryVersion}/other.tar.gz"
    ${ArchivePath}
    TLS_VERIFY ON
  )
endif()

# Extract the binaries, overriding any already present.
file(REMOVE_RECURSE ${LibRoot})
file(MAKE_DIRECTORY ${LibRoot})
execute_process(
  COMMAND ${CMAKE_COMMAND} -E tar xzf ${ArchivePath}
  WORKING_DIRECTORY ${LibRoot}
)

# List of absolute paths to libraries that should be bundled with the plugin.
# This list could contain prebuilt libraries, or libraries created by an
# external build triggered from this build file.
set(flutter_fuelet_smart_contract_wallet_bundled_libraries
  "${LibRoot}/${FLUTTER_TARGET_PLATFORM}/libfuelet_smart_contract_wallet.so"
  PARENT_SCOPE
)