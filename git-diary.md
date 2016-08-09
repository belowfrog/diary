# 生成git秘钥
1. 检查秘钥是否生成`ll ~/.ssh`
2. 设置用户名密码
  ```
  git config --global user.name "xxx"
  git config --global user.email "xxx"
  ```
3. 生成秘钥`ssh-keygen -t rsa -C “xxx”`
4. 添加秘钥到ssh `ssh-add xxx`
5. 在github中添加公钥

# 提交代码时还需要输入密码
1. 从git clone的项目还是需要输入密码
2. 修改remote url为ssh方式
3. 修改
  ```
  vim .git/config
  修改[remote original]
  url = git@github.com:xxx/xxx
  ```
