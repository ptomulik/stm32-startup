#
# Copyright (c) 2013 by Pawel Tomulik <ptomulik@meil.pw.edu.pl>
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

Import(['env', 'options'])

local_opts =  [ 
    'CMSIS_BASEDIR',
    'MCU_CORE',
    'MCU_FAMILY',
    'MCU_TARGET',
    'SCONSCRIPT_TARGET',
    'STDPERIPH_BASEDIR',
]

# 
# Supported MCU targets
#
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

#
# Mapping the supported MCU targets to their families
#
mcu_family_dict = {
    # STM32F10x LD performance line
    'STM32F103X4' : 'STM32F10X',
    'STM32F103X6' : 'STM32F10X',
    # STM32F10x MD performance line
    'STM32F103X8' : 'STM32F10X',
    'STM32F103XB' : 'STM32F10X',
    # STM32F10x HD performance line
    'STM32F103XC' : 'STM32F10X',
    'STM32F103XD' : 'STM32F10X',
    'STM32F103XE' : 'STM32F10X',
    # STM32F10x XL performance line
    'STM32F103XF' : 'STM32F10X',
    'STM32F103XG' : 'STM32F10X',
    # STM23F10x connectivity line
    'STM32F105X8' : 'STM32F10X',
    'STM32F105XB' : 'STM32F10X',
    'STM32F105XC' : 'STM32F10X',
    'STM32F107X8' : 'STM32F10X',
    'STM32F107XB' : 'STM32F10X',
    'STM32F107XC' : 'STM32F10X',
}

#
# Mapping MCU family to appropriate cortex core
#
mcu_core_dict = {
    'STM32F10X' : 'cortex-m3',
    'STM32F4XX' : 'cortex-m4',
}

startup_subs = {
    # LD PERFORMANCE LINE
    'STM32F103X4' : { '@FLASH@' : '16K',  '@RAM@' : '6K',  '@STACK@' : '1K' },
    'STM32F103X6' : { '@FLASH@' : '32K',  '@RAM@' : '10K', '@STACK@' : '1K' },
    # MD PERFORMANCE LINE
    'STM32F103X8' : { '@FLASH@' : '64K',  '@RAM@' : '20K', '@STACK@' : '1K' }, 
    'STM32F103XB' : { '@FLASH@' : '128K', '@RAM@' : '20K', '@STACK@' : '1K' },
    # HD PERFORMANCE LINE
    'STM32F103XC' : { '@FLASH@' : '256K', '@RAM@' : '48K', '@STACK@' : '1K' },
    'STM32F103XD' : { '@FLASH@' : '384K', '@RAM@' : '64K', '@STACK@' : '1K' },
    'STM32F103XE' : { '@FLASH@' : '512K', '@RAM@' : '64K', '@STACK@' : '1K' },
    # XL PERFORMANCE LINE
    'STM32F103XF' : { '@FLASH@' : '768K', '@RAM@' : '96K', '@STACK@' : '1K' },
    'STM32F103XG' : { '@FLASH@' : '1M',   '@RAM@' : '96K', '@STACK@' : '1K' },
    # CONNECTIVITY LINE
    'STM32F105X8' : { '@FLASH@' : '64K',  '@RAM@' : '64K', '@STACK@' : '1K' },
    'STM32F105XB' : { '@FLASH@' : '128K', '@RAM@' : '64K', '@STACK@' : '1K' },
    'STM32F105XC' : { '@FLASH@' : '256K', '@RAM@' : '64K', '@STACK@' : '1K' },
    'STM32F107X8' : { '@FLASH@' : '64K',  '@RAM@' : '64K', '@STACK@' : '1K' },
    'STM32F107XB' : { '@FLASH@' : '128K', '@RAM@' : '64K', '@STACK@' : '1K' },
    'STM32F107XC' : { '@FLASH@' : '256K', '@RAM@' : '64K', '@STACK@' : '1K' },
}

# Dict used to generate dependencies on stm32f10x_{xx}.S files.
stm32f10x_line_dict = {
    # LD performance line
    'stm32f103x4' : 'xx',
    'stm32f103x6' : 'xx',
    # MD performance line
    'stm32f103x8' : 'xx',
    'stm32f103xb' : 'xx',
    # HD performance line
    'stm32f103xc' : 'xx',
    'stm32f103xd' : 'xx',
    'stm32f103xe' : 'xx',
    # XL performance line
    'stm32f103xf' : 'xl',
    'stm32f103xg' : 'xl',
    # connectivity line
    'stm32f105x8' : 'cl',
    'stm32f105xb' : 'cl',
    'stm32f105xc' : 'cl',
    'stm32f107x8' : 'cl',
    'stm32f107xb' : 'cl',
    'stm32f107xc' : 'cl'
}

#
# Split 'options' into environment overrides and local options.
#
ovrr = dict([(k,v) for k,v in options.iteritems() if k not in local_opts])
opts = dict([(k,v) for k,v in options.iteritems() if k in local_opts])

#
# MCU_TARGET
#
try:             mcu_target = opts['MCU_TARGET']
except KeyError: raise SCons.Errors.UserError('You must specify MCU_TARGET')
if not mcu_target.upper() in mcu_targets:
    raise SCons.Errors.UserError('unsupported MCU_TARGET: %s' % mcu_target)
mcu_target = mcu_target.upper()
model      = mcu_target.lower()

#
# MCU_FAMILY
#
mcu_family = opts.get('MCU_FAMILY', mcu_family_dict[mcu_target])
mcu_family = mcu_family.upper()
family     = mcu_family.lower()

#
# MCU_CORE
#
mcu_core = opts.get('MCU_CORE', mcu_core_dict[mcu_family])
mcu_core = mcu_core.lower()
if mcu_core:    mcu_flags = ['-mcpu=%s' % mcu_core, '-mthumb']
else:           mcu_flags = []

#
# ASFLAGS
#
asflags = ovrr.get('ASFLAGS', env.get('ASFLAGS', []))
asflags = asflags[:] # make a copy
asflags += mcu_flags
#asflags += []
ovrr['ASFLAGS'] = asflags

#
# CPPDEFINES
#
cppdefs = ovrr.get('CPPDEFINES', env.get('CPPDEFINES',[]))
cppdefs = cppdefs[:] # make a copy
#if 'USE_STDPERIPH_DRIVER' not in cppdefs: cppdefs.append('USE_STDPERIPH_DRIVER')
#if mcu_target not in cppdefs:             cppdefs.append(mcu_target)
ovrr['CPPDEFINES'] = cppdefs

#
# CPPPATH
#
cpppath = ovrr.get('CPPPATH', env.get('CPPPATH',[]))
cpppath = cpppath[:] # make a copy
cpppath += ['src/%s' % family]
ovrr['CPPPATH'] = cpppath

#
# LINKFLAGS
#
linkflags = ovrr.get('LINKFLAGS', env.get('LINKFLAGS', []))[:]
linkflags = linkflags[:] # make a copy
linkflags += mcu_flags
ovrr['LINKFLAGS'] = linkflags

subst_dict = startup_subs[mcu_target].copy()
lib_name = 'startup_%s' % model  # name of the generated library
lds_name = '%s.ld'      % model  # name of the generated linker script
subst_dict['@LIB@'] = lib_name

#
# Build the library
#
lib = env.Library(lib_name, 'src/%s/%s.S' % (family, model), **ovrr)

#
# Correct dependencies
#
common = [ 'src/%s/%s_%s.S' % (family,s,family) for s in ['head','tail','nvic']]
env.Depends(lib, common)
# Dependencies specific to STM32F10x family.
if family == 'stm32f10x':
    line = stm32f10x_line_dict[model]
    env.Depends(lib, ['src/%s/nvic_%s_%s.S' % (family, family, line)])

#
# Generate linker script
#
substkw = { 'SUBST_DICT' : subst_dict }
lds = env.Substfile(lds_name, 'src/%s/%s.ld.in' % (family, family), **substkw)
target = lib + lds

#
# RETURN WHAT WAS BUILT
#
Return('target')

# Local Variables:
# # tab-width:4
# # indent-tabs-mode:nil
# # End:
# vim: set syntax=scons expandtab tabstop=4 shiftwidth=4:
