cmake_minimum_required (VERSION 3.0.2) 
 
function(AddRpcCore Directory)
    message("[${Directory}]")
    add_library(${Directory} SHARED
               # ComInternals.c
                RpcCore.c
                ../RpcCommon/ntdll.c
                ../RpcCommon/Misc.c
                RpcCore.def
                RpcCoreResource.rc
                )
    
    target_include_directories(
        ${Directory} PUBLIC
        ${Directory}
        )
endfunction(AddRpcCore)

file(GLOB CoreFiles *)
foreach(Files ${CoreFiles})
    if (IS_DIRECTORY ${Files} )
    
        get_filename_component(Dir ${Files} NAME)

        if(${CMAKE_GENERATOR_PLATFORM} MATCHES "x64")
            AddRpcCore(${Dir})
        else()
            if(${Dir} MATCHES "32bits")
                AddRpcCore(${Dir})
            endif(${Dir} MATCHES "32bits")
        endif()
    endif (IS_DIRECTORY ${Files} )
endforeach(Files)