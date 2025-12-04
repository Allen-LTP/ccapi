set(NAME ltp_trading_example)
project(${NAME})
add_compile_definitions(CCAPI_ENABLE_SERVICE_EXECUTION_MANAGEMENT)
# add_compile_definitions(CCAPI_ENABLE_EXCHANGE_BINANCE)
add_compile_definitions(CCAPI_ENABLE_EXCHANGE_BINANCE_USDS_FUTURES)
# add_compile_definitions(CCAPI_ENABLE_EXCHANGE_BINANCE_COIN_FUTURES)
# add_compile_definitions(CCAPI_ENABLE_EXCHANGE_BINANCE_PORTFOLIO_MARGIN)
# add_compile_definitions(CCAPI_ENABLE_EXCHANGE_OKX)
# add_compile_definitions(CCAPI_ENABLE_EXCHANGE_BYBIT)
# add_compile_definitions(CCAPI_ENABLE_EXCHANGE_HUOBI)

add_definitions(-DCCAPI_ENABLE_LOG_INFO)

get_filename_component(CCAPI_PROJECT_DIR ../../.. ABSOLUTE)

include_directories(${CCAPI_PROJECT_DIR}/example/src)

add_executable(${NAME} main.cpp)
add_dependencies(${NAME} boost rapidjson)

link_directories(/usr/local/lib)
target_link_libraries(${NAME} ucli_ffi pthread ssl crypto)

set_target_properties(${NAME} PROPERTIES
    BUILD_RPATH "/usr/local/lib"
    INSTALL_RPATH "/usr/local/lib"
    BUILD_WITH_INSTALL_RPATH TRUE
)

set(NAME_STRESS ltp_trading_stress_test)
add_executable(${NAME_STRESS} stress_test.cpp)
add_dependencies(${NAME_STRESS} boost rapidjson)

target_link_libraries(${NAME_STRESS} ucli_ffi pthread ssl crypto)

set_target_properties(${NAME_STRESS} PROPERTIES
    BUILD_RPATH "/usr/local/lib"
    INSTALL_RPATH "/usr/local/lib"
    BUILD_WITH_INSTALL_RPATH TRUE
)