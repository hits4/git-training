# git-training


## ���|�W�g���̍쐬/�N���[��

###���[�J���Ƀ��|�����
git init

###clone
$ git clone https://github.com/schacon/ticgit


---
## �R�~�b�g
### git��commit�̂�蒼��(�㏑��)�R�}���h
$ git commit --amend

### amend�̎g����
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend


### add����commit
git commit -a -m 'added new benchmarks'

### �ǐՑΏۂ���폜
git rm

### �t�@�C���͎c���ĒǐՑΏ�������폜
$ git rm --cached README

## �����[�g�̑���

## push 
$ git push origin master

---

## �}�[�W/�����Ǘ�
GUI��diff����
$git difftool

difftool��.gitconfig�ł��炩���ߐݒ肵�Ă���

--- 
## ���[�U�[�Ǘ��ƃp�X���[�h

### �u���i���}�l�[�W���v�̖�����
windows��git�͔F�؏���windows�́u���i���}�l�[�W���v�ŊǗ����Ă��܂��B
���ꂪ�L�����ƁA.config��user��񂪖�������Ă��܂��̂ŁA�����ɂ���B
git config --system -e

https://qiita.com/tyori03/items/3cc2915f7429251eb908

### �p�X���[�h�̕ۑ�
git config --global credential.helper store
