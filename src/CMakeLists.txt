include_directories(${libzmq_SOURCE_DIR}/include)
include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${CMAKE_CURRENT_BINARY_DIR})
include(CheckIncludeFiles)
include(CheckFunctionExists)

check_include_files("alloca.h" HAVE_ALLOCA_H)
check_include_files("arpa/inet.h" HAVE_ARPA_INET_H)
check_function_exists("clock_gettime" HAVE_CLOCK_GETTIME)
if(WIN32)
	set(ZMQ_HAVE_WINDOWS 1)
endif(WIN32)
if(MINGW)
	set(ZMQ_HAVE_MINGW32 1)
endif(MINGW)
if(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
	set(ZMQ_HAVE_LINUX 1)
endif(${CMAKE_SYSTEM_NAME} MATCHES "Linux")

if(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
	set(ZMQ_HAVE_OSX 1)
endif(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/platform.hpp.cmakein ${CMAKE_CURRENT_BINARY_DIR}/platform.hpp)

set(libzmq_la_SOURCES
    clock.cpp  
    ctx.cpp  
    decoder.cpp  
    devpoll.cpp  
    dist.cpp  
    encoder.cpp  
    epoll.cpp  
    err.cpp  
    fq.cpp  
    io_object.cpp  
    io_thread.cpp  
    ip.cpp  
    ipc_address.cpp  
    ipc_connecter.cpp  
    ipc_listener.cpp  
    kqueue.cpp  
    lb.cpp  
    mailbox.cpp  
    msg.cpp  
    mtrie.cpp  
    object.cpp  
    options.cpp  
    own.cpp  
    pair.cpp  
    pgm_receiver.cpp  
    pgm_sender.cpp  
    pgm_socket.cpp  
    pipe.cpp  
    poll.cpp  
    poller_base.cpp  
    pull.cpp  
    push.cpp  
    reaper.cpp  
    pub.cpp  
    random.cpp  
    rep.cpp  
    req.cpp  
    select.cpp  
    session_base.cpp  
    signaler.cpp  
    socket_base.cpp  
    stream_engine.cpp  
    sub.cpp  
    tcp_address.cpp  
    tcp_connecter.cpp  
    tcp_listener.cpp  
    thread.cpp  
    trie.cpp  
    xpub.cpp  
    xrep.cpp  
    xreq.cpp  
    xsub.cpp  
    zmq.cpp  
    zmq_utils.cpp
)

add_library(zmq ${libzmq_la_SOURCES})
