###############################################################################
# Copyright (c) 2014-2019, Lawrence Livermore National Security, LLC.
# 
# Produced at the Lawrence Livermore National Laboratory
# 
# LLNL-CODE-666778
# 
# All rights reserved.
# 
# This file is part of Conduit. 
# 
# For details, see: http://software.llnl.gov/conduit/.
# 
# Please also read conduit/LICENSE
# 
# Redistribution and use in source and binary forms, with or without 
# modification, are permitted provided that the following conditions are met:
# 
# * Redistributions of source code must retain the above copyright notice, 
#   this list of conditions and the disclaimer below.
# 
# * Redistributions in binary form must reproduce the above copyright notice,
#   this list of conditions and the disclaimer (as noted below) in the
#   documentation and/or other materials provided with the distribution.
# 
# * Neither the name of the LLNS/LLNL nor the names of its contributors may
#   be used to endorse or promote products derived from this software without
#   specific prior written permission.
# 
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
# AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
# IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
# ARE DISCLAIMED. IN NO EVENT SHALL LAWRENCE LIVERMORE NATIONAL SECURITY,
# LLC, THE U.S. DEPARTMENT OF ENERGY OR CONTRIBUTORS BE LIABLE FOR ANY
# DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL 
# DAMAGES  (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS
# OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
# HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, 
# STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING
# IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE 
# POSSIBILITY OF SUCH DAMAGE.
# 
###############################################################################

################################
# Conduit Unit Tests
################################

################################
# Docs Related Unit Tests
################################
set(DOCS_TESTS  
    t_conduit_docs_tutorial_basics
    t_conduit_docs_tutorial_numeric
    t_conduit_docs_tutorial_parse
    t_conduit_docs_tutorial_ownership
    t_conduit_docs_tutorial_errors
    t_conduit_docs_relay_io_generic_examples
    t_conduit_docs_blueprint_examples
    t_conduit_docs_blueprint_demos)

set(DOCS_HDF5_TESTS  
    t_conduit_docs_relay_io_handle_examples
    t_conduit_docs_relay_io_hdf5_examples)


set(DOCS_PYTHON_TESTS  
    t_conduit_docs_tutorial_python_basics
    t_conduit_docs_tutorial_python_numeric
    t_conduit_docs_tutorial_python_parse
    t_conduit_docs_tutorial_python_ownership
    t_conduit_docs_tutorial_python_relay_io_handle_examples)

set(DOCS_PYTHON_MPI_TESTS  
    t_conduit_docs_tutorial_python_relay_mpi_examples)


################################
# Add our tests
################################
message(STATUS "Adding docs related unit tests")
foreach(TEST ${DOCS_TESTS})
    add_cpp_test(TEST ${TEST}
                 DEPENDS_ON conduit conduit_blueprint conduit_relay
                 FOLDER tests/docs)
endforeach()

################################
# Add HDF5 Tests
################################
if(HDF5_FOUND)
    foreach(TEST ${DOCS_HDF5_TESTS})
        add_cpp_test(TEST ${TEST}
                     DEPENDS_ON conduit conduit_blueprint conduit_relay
                     FOLDER tests/docs)
    endforeach()
endif()

################################
# Add Python Tests
################################
if(PYTHON_FOUND)
    foreach(TEST ${DOCS_PYTHON_TESTS})
        add_python_test(TEST ${TEST}
                        FOLDER tests/docs)
    endforeach()

    if(MPI_FOUND)
        foreach(TEST ${DOCS_PYTHON_MPI_TESTS})
            add_python_mpi_test(TEST ${TEST}
                                NUM_MPI_TASKS 2)
                                # FOLDER tests/docs)
        endforeach()
    endif()

else()
    message(STATUS "Python disabled: Skipping conduit python tutorial examples")
endif()




