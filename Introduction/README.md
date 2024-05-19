---
title: 'Git Introduction & Common Operations'
disqus: hackmd
---

Git Introduction & Common Operations
===

# Table of Contents

[TOC]

# git Introduction
> [!NOTE]
>Git 是一個分散式版本控制系统，最初由Linus Torvalds為了更好地管理Linux内核開發而創建。允許多人協作開發項目，追蹤文件的編輯紀錄，以及管理版本的變化。
>
>
>1. **分散式版本控制系统**：
>每個使用Git的使用者都擁有完整的code base的副本。這也意旨即使伺服器發生故障，開發者仍然可以繼續工作。
>2. **版本控制**：
>Git追蹤文件的編輯紀錄，允許開發者紀錄項目的不同版本。這使得可以隨時返回到先前的狀態，查看特定版本之間的差異。
>3. **分支（Branch）**：
>Git允許創建分支，即獨立的開發路徑。可以在不影響主線(Main)開發的情况下進行實驗性開發、修復bug等。分支可以合併回主線開發。
>4. **提交（Commit）**：
>將文件的修改保存到Git的過程。每次提交都包含一個提交資訊，描述了當次修改的内容。
>5. **合併（Merge）**：
>將一個分支的更改合併到另一個分支。當一個分支的開發完成後，可以將其合併回主線開發。
>6. **Others**:
>Clone、Pull、Push、Tag ...

![image](https://hackmd.io/_uploads/HkcefFzg0.png)


# Install
Git download: https://git-scm.com/downloads/
> git bash
# Config
● Initialize data
```command
 git init
```
● Configure your personal information
```command
 git config --global user.name "Your Name"
 git config --global user.name "your.email@example.com"
```
● Check the configured user information
```command
git config --list
```

![image](https://hackmd.io/_uploads/HyDilE_kR.png)

# Git editing process
![image](https://hackmd.io/_uploads/rylLqtGxA.png)

> [!TIP]
>Situation:\
>這裡有一份空白的國小數學考券 "paper.txt"\
>(一) 填空題 (55%)
>1. 1 + 1 = __ (5 pts)
>2. 5 x 7 = __ (10 pts)
>3. 9 + 6 = __ (10 pts)
>4. 8 - 3 = __ (10 pts)
>5. 12 ÷ 4 = __ (10 pts)
>6. 10 x 10 = __ (10 pts)
>
>(二) 簡答題 (45%)
>1. 你有10個蘋果，吃掉了2個，媽媽又給你6個，你還剩下幾個？__ (15 pts)
>2. 如果跑步比賽，你跑贏了第2名，請問你是第幾名？__ (15 pts)
>3. 10人搭公車7人下車，剩幾人？__ (15 pts)

# Completed oneself
## 1. Create paper.txt
```command
vi paper.txt
```
paper.txt:
```txt=
(一) 填空題 (55%)
1. 1 + 1 = __ (5 pts)
2. 5 x 7 = __ (10 pts)
3. 9 + 6 = __ (10 pts)
4. 8 - 3 = __ (10 pts)
5. 12 ÷ 4 = __ (10 pts)
6. 10 x 10 = __ (10 pts)

(二) 簡答題 (45%)
1. 你有10個蘋果，吃掉了2個，媽媽又給你6個，你還剩下幾個？__ (15 pts)
2. 如果跑步比賽，你跑贏了第2名，請問你是第幾名？__ (15 pts)
3. 10人搭公車7人下車，剩幾人？__ (15 pts)
```

```command
<esc>:wq! #store and quit
```
## 1.1 Changes request
```command
git add .  //add changes in the current directory to the staging area
git status //overview of what changes you've made
```
![image](https://hackmd.io/_uploads/S1dZb4u10.png)

```command
git commit -m "add paper.txt" 
```
> Create a new commit in the Git repository
> The commit message: "add paper.txt"

![image](https://hackmd.io/_uploads/BymUbE_JC.png)

● Return to confirm the status
```command
git status
```
![image](https://hackmd.io/_uploads/H1VPWVuJ0.png)
> It's empty.
> Cause the changes be committed

● Check git log
```command
git log
```
![image](https://hackmd.io/_uploads/SJGtZ4dkR.png)

![image](https://hackmd.io/_uploads/B1l5-E_J0.png)


## 2. Complete the first question
```
vim paper.txt
```
paper.txt:
```txt=
(一) 填空題 (55%)
1. 1 + 1 = _2_ (5 pts)
2. 5 x 7 = __ (10 pts)
```
```command
<esc>:wq! #store and quit
```
## 2.1 Changes request
```command
git add paper.txt  //add changes in the paper.txt to the staging area
git status
```
![image](https://hackmd.io/_uploads/SyjzMN_10.png)

```command
git commit -m "Complete problem 1"
```
![image](https://hackmd.io/_uploads/SkbVz4OJR.png)
```command
git log
```
![image](https://hackmd.io/_uploads/HJ5BME_1A.png)

# Branch
> [!TIP]
>Situation:\
>已建完考券 且 完成第一題。\
>接著交給:
>
> ◆ **Alice完成剩下的第一大題:**\
>(一) 填空題 (55%)
>1. 1 + 1 = _2_ (5 pts)
>2. 5 x 7 = __ (10 pts)
>3. 9 + 6 = __ (10 pts)
>4. 8 - 3 = __ (10 pts)
>5. 12 ÷ 4 = __ (10 pts)
>6. 10 x 10 = __ (10 pts)
>
>◆ **Bob完成第二大題:**\
>(二) 簡答題 (45%)
>1. 你有10個蘋果，吃掉了2個，媽媽又給你6個，你還剩下幾個？__ (15 pts)
>2. 如果跑步比賽，你跑贏了第2名，請問你是第幾名？__ (15 pts)
>3. 10人搭公車7人下車，剩幾人？__ (15 pts)

![image](https://hackmd.io/_uploads/BJRX8iMxC.png)

## 1. Create & Switch Branch
### ● Create & Switch to alice
```command
git checkout -b alice
```
![image](https://hackmd.io/_uploads/Bk4_GVOyR.png)

### ● Create & Switch to bob
```command
 git checkout master //back to master branch
```
> back to master and add another branch\
![image](https://hackmd.io/_uploads/B10sGVuy0.png)
```command
git checkout bob
```
![image](https://hackmd.io/_uploads/ryVTGVOJ0.png)

```command
git status
```
![image](https://hackmd.io/_uploads/HJlJ7V_yR.png)


## 2. Branch alice
### 2.1 Switch to alice
```command
git checkout alice
```
![image](https://hackmd.io/_uploads/Syifm4d1R.png)
### 2.2 alice editing
```command
 vi paper.txt
```
```txt=
(一) 填空題 (55%)
1. 1 + 1 = _2_ (5 pts)
2. 5 x 7 = _35_ (10 pts) 
3. 9 + 6 = _15_ (10 pts)
4. 8 - 3 = _5_ (10 pts)
5. 12 ÷ 4 = _3_ (10 pts)
6. 10 x 10 = _100_ (10 pts)

(二) 簡答題 (45%)
1. 你有10個蘋果，吃掉了2個，媽媽又給你6個，你還剩下幾個？_ (15 pts)
2. 如果跑步比賽，你跑贏了第2名，請問你是第幾名？_ (15 pts)
3. 10人搭公車7人下車，剩幾人？_ (15 pts)
```
```command
<esc>:wq! #store and quit
```
### 2.3 Changes request
```command
git add paper.txt
git status
```
![image](https://hackmd.io/_uploads/HJ9sXNuyA.png)

```command
git commit -m "Complete alice done"
```
![image](https://hackmd.io/_uploads/Sk7a7V_1C.png)

## 3. Branch bob
### 3.1 Switch to bob
```command
git checkout bob
```
![image](https://hackmd.io/_uploads/HyukNE_1R.png)

> [!CAUTION]
>**Unable to see the commit history of other branches**

● check paper.txt file & git log
```command
cat paper.txt
```
![image](https://hackmd.io/_uploads/SkzMVVO1C.png)
> It's a original file.

```command
git log
```
![image](https://hackmd.io/_uploads/rkyOVNuJC.png)
> No log with "Complete alice done"\
> Also none in branch Master.\
> ![image](https://hackmd.io/_uploads/ry8ANN_k0.png)

### 3.2 Bob editing
```command
vi paper.txt
```
```txt=
(一) 填空題 (55%)
1. 1 + 1 = __ (5 pts)
2. 5 x 7 = __ (10 pts) 
3. 9 + 6 = __ (10 pts)
4. 8 - 3 = __ (10 pts)
5. 12 ÷ 4 = __ (10 pts)
6. 10 x 10 = __ (10 pts)

(二) 簡答題 (45%)
1. 你有10個蘋果，吃掉了2個，媽媽又給你6個，你還剩下幾個？_14_ (15 pts)
2. 如果跑步比賽，你跑贏了第2名，請問你是第幾名？_2_ (15 pts)
3. 10人搭公車7人下車，剩幾人？_4_ (15 pts)
```
```command
<esc>:wq! #store and quit
```
### 2.3 Changes request
```command
 git add paper.txt
 git status
```
![image](https://hackmd.io/_uploads/BJPfHEu1R.png)

```command
 git commit -m "Complete bob done"
```
![image](https://hackmd.io/_uploads/S1imHEd1R.png)

```command
 git log
```
![image](https://hackmd.io/_uploads/BJRBH4OJC.png)
> There is "Complete bob done",but no alice.
> Because of different branches.

# Merge
> [!TIP]
>Situation:\
>依照上述步驟:
>
>◆ Alice 先完成第一大題\
>◆ Bob 後完成第二大題

新情境:
雖然Alice先完成，但Bob先交卷
:::
## ● Return to Master and Merge
### 1. Merge Bob
```command
git checkout master
git merge bob
```
![image](https://hackmd.io/_uploads/H113BVu10.png)

```command
git log
```
![image](https://hackmd.io/_uploads/B1f0HEdy0.png)
### 2. Merge Alice
```command
git merge alice
```
![image](https://hackmd.io/_uploads/B1flLEuJR.png)

```
 git log
```
![image](https://hackmd.io/_uploads/ryo48E_yC.png)

> [!IMPORTANT]
>"Successfully completed the branch task."

# Connecting to GitHub: SSH
## SSH key
### 1. Generate SSH key pairs for secure communication
```
ssh-keygen
```

![image](https://hackmd.io/_uploads/HkS2UE_1A.png)
> Enter passphrase (empty for no passphrase):
> optional but recommended for additional security
### 2. Default location to save the key pair
```
cat ~/.ssh/id_rsa.pub
```
> ssh-rsa: A type of cryptographic algorithm used in SSH (Secure Shell) for authentication and encryption.

## Github: Settings >> SSH and GPG keys
https://github.com/settings/keys
> [!NOTE]
>GitHub supports two types of keys for secure communication and authentication: SSH keys and GPG (GNU Privacy Guard) keys.

![image](https://hackmd.io/_uploads/H1TSDNdkA.png)

### Paste the id_rsa.pub
![image](https://hackmd.io/_uploads/SyDtDEOyA.png)

## Verify
```
ssh -T git@github.com
```
![image](https://hackmd.io/_uploads/HksnDEd1R.png)

> [!IMPORTANT]
> Finally,Push the committed changes to the remote GitHub repository.

![S__504643588](https://hackmd.io/_uploads/BJ4SIxEeA.jpg)

