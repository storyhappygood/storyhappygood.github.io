# 分子模拟——mdtraj学习

mdtraj是分子动力学模拟的一个python包，类似的包还有mdannalysis.

官网地址：http://mdtraj.org/

## 安装：

使用conda进行安装：

'''
conda install -c conda-forge mdtraj
'''

pip 安装：

'''
pip install mdtraj
'''

测试安装：

'''
pip install nose
'''

测试：

'''
nosetests mdtraj -v
'''

## 使用

这段文字提供一系列的例子，资源和代码来帮助使用mdtraj

如果是通过编译安装的mdtraj可以进入path-to-mdtraj/examples查看，如果是一键安装，可以通过Github进行查看，其为Ipython notebook格式。

首先从硬盘中加载轨迹，MDTraj会自动的使用最合适的方式加载不同的文件格式。

'''
import mdtraj as md

t=md.load('trajectory.xtc',top='trajectory.pdb')

print(t)

<mdtraj.Trajectory with 100 frames, 22 atoms at 0x109f0a3d0>
'''

一些轨迹例如Gromacs XTC轨迹文件并不包含拓扑信息，我们需要采用top关键字来加载拓扑文件，例如PDB文件.

如果你只对部分轨迹感兴趣，你可以切割（slice）他们.

'''

#查看十帧（frames）
print(t[1:10])

<mdtraj.Trajectory with 9 frames, 22 atoms at 0x109b91310>

#查看最后一帧

print(t[-1])

<mdtraj.Trajectory with 1 frames, 22 atoms at 0x109b97810>

'''

轨迹对象包含许多对象，最多的显然是笛卡尔坐标——作为numpy array存储在xyz下。轨迹中的距离单位均为纳米，时间单位均为皮秒，角度存储都是度（不是弧度）。

'''
print(t.xyz.shape)

(100,22,3)

print(np.mean(t.xyz))

0.89365752249053032

#第一个十帧时间模拟

print(t:10)

array([ 0.002,  0.004,  0.006,  0.008,  0.01 ,  0.012,  0.014,  0.016,0.018,  0.02 ], dtype=float32)

#最后一帧的晶胞长度

t.unitcell_lengths[-1]

array([ 2.,  2.,  2.], dtype=float32)

'''

保存轨迹到文件也非常容易操作
'''
t[::2].save('halftraj.h5')

#个人推荐,保存成dcd格式
t[0:10].save_dcd('first-ten-frames.dcd')
'''

轨迹包含拓扑对象的引用，这可以派上用场。例如，如果你想保存你的轨迹一份只含有α碳原子的轨迹，你可以这样做:

'''
atoms_to_keep=[a.index for a in t.topology.atoms if a.name == 'CA']

t.restrict_atoms(atoms_to_keep) #在轨迹中扮演适当的作用

t.save('CA-only.h5')

'''

## 选择原子

加载轨迹

'''python
from __future__ import print_function

import mdtraj as md

traj = md.load('ala2.h5')

print(traj)

<mdtraj.Trajectory with 100 frames, 22 atoms, 3 residues, without unitcells>

'''

我们可以使用traj.n_atoms和traj.n_residues来直接的测出多少原子或残基

'''
print('多少原子? %s' % traj.n_atoms)

print('多少残基? %s' % traj.n_residues)

'''
我们同样可以使用traj.xyz来操作原子的位置，traj.xyz是一个Numpy array包含每个原子维度上的xyz坐标(n_frames, n_atoms, 3)。让我们找出第五帧的第十个原子的3维坐标。

'''
frame_idx = 4 #零开始索引，下同

atom_idx=9

print('第五帧第10个原子的位置在哪里？')

print('x:%s\ty:%s\tz:%s'%tuple(traj.xyz[frame_idx, atom_idx,:])))
'''

## 拓扑对象

就如之前所介绍的那样，每个轨迹对象都包含有拓扑。轨迹的拓扑包含所有的信息，链，残基，原子，键。

'''

topology=traj.topology

print(topology)

<mdtraj.Topology with 1 chains, 3 residues, 22 atoms, 21 bonds>


'''

在拓扑对象中我们可以选择一个清晰的原子或者loop环（注意:所有均从0开始索引）

'''

print('Fifth atom: %s' % topology.atom(4))

print('All atoms: %s' % [atom for atom in topology.atoms])

'''

Fifth atom: ACE1-C

All atoms: [ACE1-H1, ACE1-CH3, ACE1-H2, ACE1-H3, ACE1-C, ACE1-O, ALA2-N, ALA2-H, ALA2-CA, ALA2-HA, ALA2-CB, ALA2-HB1, ALA2-HB2, ALA2-HB3, ALA2-C, ALA2-O, NME3-N, NME3-H, NME3-C, NME3-H1, NME3-H2, NME3-H3]

残基同样如此

'''

print('Second residue: %s' % traj.topology.residue(1))

print('All residues: %s' % [residue for residue in traj.topology.residues])

'''

Second residue: ALA2

All residues: [ACE1, ALA2, NME3]

所有的原子和残基同样拥有对象，拥有自己的属性集。这里有一些简单的例子:

'''

atom = topology.atom(10)

print('''Hi! I am the %sth atom, and my name is %s. 

I am a %s atom with %s bonds. 

I am part of an %s residue.''' % ( atom.index, atom.name, atom.element.name, atom.n_bonds, atom.residue.name))

'''

Hi! I am the 10th atom, and my name is CB.

I am a carbon atom with 4 bonds.

I am part of an ALA residue.

同样还有一些复杂的参数，例如atoms.is_sidechain 或者residue.is_protein,允许有更多的选择

## 大杂烩

你可以看到这些参数是如何和python的筛选功能结合在一起的。比如我们想查看我们分子侧链的所有碳原子，我们可以尝试这样.

'''

print([atom.index for atom in topology.atoms if atom.element.symbol is 'C' and atom.is_sidechain])

'''

或者我们想索引第一条链的所有奇数残基

'''

print([residue for residue in topology.chain(0).residues if residue.index % 2 == 0])

'''

## 原子选择语法

MDTraj拥有和PyMol和VMD类似的原子选择语法，你可以使用topology.select来使用，让我们查找前两个残基的所有原子。

在主文档中含有更多信息

'''

print(topology.select('resid 1 to 2'))

'''

[ 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21]

