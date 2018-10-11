# -*- coding:utf-8 –*-
# @File:   Sconscript
# @Author: buildpkg.exe
# @Date:   2018-09-19 18:07:00(The date the template was created)
#
# @LICENSE: https://github.com/rtpkgs/buildpkg/blob/master/LICENSE.
#
# Change Logs:
# Date           Author         Notes 
# 20xx-xx-xx     buildpkg.exe   auto create by buildpkg.exe. 

import os
from building import * 

# Get current dir path
cwd = GetCurrentDir()

# Init inc_list and src_list vars
inc = [] 
src = []

# debug info
print(inc)
print(src)

# Remove ignore src and 
list_ignore_inc = []
list_ignore_src = []

# --------------------------------------------------------------------------------
#  user add ignore: 
# --------------------------------------------------------------------------------
list_ignore_inc += [] 
list_ignore_src += []

# --------------------------------------------------------------------------------
#  auto add ignore: 
# --------------------------------------------------------------------------------
list_ignore_inc += ['.git', 'example', 'doc', 'test'] 
list_ignore_src += ['test.c', 'example.c'] 

# Traverse package, add code and path to project 
def traverse_package(f):
    fs = os.listdir(f) 
    for f1 in fs: 
        tmp_path = os.path.join(f, f1) 
        filename = os.path.basename(tmp_path)

        if os.path.isdir(tmp_path): # dir
            if not filename in list_ignore_inc: 
                print("DIR: " + filename)
                inc.append(f)
                traverse_package(tmp_path)
        else: # file
            suffix = os.path.splitext(tmp_path)[1]
            if suffix   == '.c' and not filename in list_ignore_src:
                #print("FILE: " + filename)
                src.append(tmp_path)
            elif suffix == '.h':
                inc.append(f)
            
traverse_package(cwd) 

# Add group to IDE project
objs = DefineGroup('sam-v1.0.0', src, depend = ['PKG_USING_SAM'], CPPPATH = inc)

# Traversal subscript
list = os.listdir(cwd)
if GetDepend(['PKG_USING_SAM']):
    for d in list:
        path = os.path.join(cwd, d)
        if os.path.isfile(os.path.join(path, 'SConscript')):
            objs = objs + SConscript(os.path.join(d, 'SConscript'))

Return('objs') 