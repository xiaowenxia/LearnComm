### shell
    实现了一个简单的shell功能，通过s_cmd_table中定义指令、指令说明、和实现函数即可。
#### 编译
````sh
    make
    ./shell_test
````
#### 预览
![shell_test](https://github.com/xiaowenxia/common-lib/blob/master/shell/shell.gif)

#### 指令格式
````c
    typedef struct xx_shell{
    /* command */
    const char *cmd;
    
    /* brief help text of this command */
    const char *help;
    
    /* point to the implementation of this command */
    void (* func)(uint32_t, int8_t **);
}xx_shell_t;
````
其中cmd为指令，help为指令说明，func为指令对应的执行函数。比如：
````c
    static shell = { "help","      Display list of commands.", shell_help};
````
#### API说明
shell模块初始化函数：
````c
    uint8_t cmd_init(void);
````
注册指令函数：
````c
    /* 注册单个指令 */
    uint8_t cmd_register(xx_shell_t *shell);

    /* 注册指令数组 */
    uint8_t cmd_register_array(xx_shell_t *shell, uint32_t array_size);
````
处理指令函数：
````c
    /* data为一条指令数据，必须以'/r/n'为结尾 */
    uint8_t cmd_parse(uint8_t *data);
````