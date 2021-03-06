cmake_minimum_required(VERSION 3.15)
project(InsertSortByCMake)

set(CMAKE_CXX_STANDARD 14)


function(swap INPUT first second)
    list(GET INPUT ${first} f_v)
    list(GET INPUT ${second} s_v)
    list(REMOVE_AT INPUT ${first})
    list(INSERT INPUT ${first} ${s_v})
    list(REMOVE_AT INPUT ${second})
    list(INSERT INPUT ${second} ${f_v})

    set(INPUT ${INPUT} PARENT_SCOPE)
endfunction()


function(insert_sort INPUT)
    list(LENGTH INPUT len)
    math(EXPR len "${len}-1")
    foreach(i RANGE 1 ${len})
        set(j ${i})
        while(${j} GREATER 0)
            list(GET INPUT ${j} v_j)
            math(EXPR j_1 "${j}-1")
            list(GET INPUT ${j_1} v_j_1)
            if(${v_j} GREATER ${v_j_1})
                break()
            endif()
            swap("${INPUT}" ${j} ${j_1})
            math(EXPR j "${j}-1")
        endwhile()
    endforeach()
    set(INPUT ${INPUT} PARENT_SCOPE)
endfunction()


set(INPUT 9 5 4 7 6 8 3 0 1 2)
message(INPUT= "${INPUT}")
insert_sort("${INPUT}")
message(OUTPUT= "${INPUT}")