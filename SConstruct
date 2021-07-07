import os
import sys
import rtconfig

if os.getenv('RTT_ROOT'):
    RTT_ROOT = os.getenv('RTT_ROOT')
else:
    RTT_ROOT = os.path.join(os.getcwd(), '..', '..')

sys.path = sys.path + [os.path.join(RTT_ROOT, 'tools')]
from building import *

TARGET = 'rtthread.' + rtconfig.TARGET_EXT

DefaultEnvironment(tools=[])
env = Environment(tools = ['mingw'],
    AS   = rtconfig.AS, ASFLAGS = rtconfig.AFLAGS,
    CC   = rtconfig.CC, CCFLAGS = rtconfig.CFLAGS,
    CXX  = rtconfig.CXX, CXXFLAGS = rtconfig.CXXFLAGS,
    AR   = rtconfig.AR, ARFLAGS = '-rc',
    LINK = rtconfig.LINK, LINKFLAGS = rtconfig.LFLAGS)
env.PrependENVPath('PATH', rtconfig.EXEC_PATH)
env['ASCOM'] = env['ASPPCOM']

Export('RTT_ROOT')
Export('rtconfig')

if os.getenv('BEAR_PKG_ROOT'):
    BEAR_PKG_ROOT = os.getenv('BEAR_PKG_ROOT')
else:
    print("please set BEAR_PKG_ROOT to build pakage ROOT!")
    sys.exit(-1)

Export('BEAR_PKG_ROOT')

# prepare building environment
objs = PrepareBuilding(env, RTT_ROOT)

# include libraries
objs.extend(SConscript(os.path.join(BEAR_PKG_ROOT, 'SConscript')))

# make a building
DoBuilding(TARGET, objs)
