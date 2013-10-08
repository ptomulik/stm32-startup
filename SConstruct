#
# Copyright (c) by Pawel Tomulik <ptomulik@meil.pw.edu.pl>
# 
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
# 
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
# 
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE

import os

tools = {
  'ADDR2LINE'   : 'arm-none-eabi-addr2line',
  'AR'          : 'arm-none-eabi-ar',
  'AS'          : 'arm-none-eabi-gcc',
  'CXXFILT'     : 'arm-none-eabi-c++filt',
  'CPP'         : 'arm-none-eabi-cpp',
  'CS'          : 'arm-none-eabi-cs',
  'ELFEDIT'     : 'arm-none-eabi-elfedit',
  'CXX'         : 'arm-none-eabi-g++',
  'CC'          : 'arm-none-eabi-gcc',
  'GCC_AR'      : 'arm-none-eabi-gcc-ar',
  'GCC_NM'      : 'arm-none-eabi-gcc-nm',
  'GCC_RANLIB'  : 'arm-none-eabi-gcc-ranlib',
  'GCOV'        : 'arm-none-eabi-gcov',
  'GDB'         : 'arm-none-eabi-gdb',
  'GPROF'       : 'arm-none-eabi-gprof',
  'LINK'        : 'arm-none-eabi-ld',
  'NM'          : 'arm-none-eabi-nm',
  'OBJCOPY'     : 'arm-none-eabi-objcopy',
  'OBJDUMP'     : 'arm-none-eabi-objdump',
  'RANLIB'      : 'arm-none-eabi-ranlib',
  'READELF'     : 'arm-none-eabi-readelf',
  'SIZE'        : 'arm-none-eabi-size',
  'STRINGS'     : 'arm-none-eabi-strings',
  'STRIP'       : 'arm-none-eabi-strip',
}

#
# COMMON COMPILATION FLAGS
#
common_flags = [
    '-g',
    '-Wall', 
    '-Wextra', 
    '-Werror',
    '-fmessage-length=0',
    '-funsigned-bitfields'
]

#
# ASFLAGS
#
asflags   = ['-x', 'assembler-with-cpp']
#
# CFLAGS
#
cflags    = []
#
# CXXFLAGS
#
cxxflags  = ['-fno-exceptions', '-fno-rtti']
#
# LINKFLAGS
#
linkflags = []

#
# ALL THE FLAGS TOGETHER
#
kwargs = tools.copy()
kwargs.update( ASFLAGS   = common_flags + asflags,
               CFLAGS    = common_flags + cflags,
               CXXFLAGS  = common_flags + cxxflags,
               LINKFLAGS = common_flags + linkflags )

env = Environment(ENV=os.environ, tools=['default','textfile'], **kwargs)

mcu_targets = [
    # STM32F10x LD performance line
    'STM32F103X4',
    'STM32F103X6',
    # STM32F10x MD performance line
    'STM32F103X8',
    'STM32F103XB',
    # STM32F10x HD performance line
    'STM32F103XC',
    'STM32F103XD',
    'STM32F103XE',
    # STM32F10x XL performance line
    'STM32F103XF',
    'STM32F103XG',
    # STM23F10x connectivity line
    'STM32F105X8',
    'STM32F105XB',
    'STM32F105XC',
    'STM32F107X8',
    'STM32F107XB',
    'STM32F107XC',
]

#############################################################################
# The library
#############################################################################
for mcu_target in mcu_targets:
    options = { 'MCU_TARGET' : mcu_target }
    lib = env.SConscript( 'SConscript', 
        variant_dir='build/%s' % mcu_target.lower(),
        duplicate=0, exports=['env', 'options'] )
