## 1. 如何注册GitHub账号

1. 打开[GitHub官网](https://github.com/)
2. 点击右上角的`Sign up`按钮
3. 输入用户名、邮箱、密码，点击`Create an account`按钮
4. 选择`Unlimited public repositories for free.`，点击`Continue`按钮
5. 选择`Skip this step`，点击`Submit`按钮
6. 打开邮箱，点击`Verify email address`按钮

注：用户名采用shinetech-EnglishName的格式，例如：shinetech-AndyWang

## 2. 如何创建GitHub仓库

1. 登录GitHub
2. 点击右上角的`+`按钮，选择`New repository`按钮
3. 输入仓库名称，例如：`learning-git`
4. 输入仓库描述，例如：`Learning Git`
5. 选择`Private`，点击`Create repository`按钮

## 3. 如何添加SSH Key

1. 打开Git Bash
2. 输入以下命令，生成SSH Key

```bash
ssh-keygen -t rsa -C "
```

3. 打开`C:\Users\shinetech\.ssh`目录，复制`id_rsa.pub`文件中的内容
4. 打开GitHub，点击右上角的头像，选择`Settings`按钮
5. 选择`SSH and GPG keys`，点击`New SSH key`按钮
6. 输入标题，例如：`shinetech-AndyWang`，粘贴刚才复制的内容，点击`Add SSH key`按钮