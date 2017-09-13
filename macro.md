### Template Pattern 模板模式

#### 

Name 	命令模式可以执行宏命令\(macro command\), 即多个命令的组合操作。

	命令模式+组合模式。

意图	

适用性	

参与者	

![](/assets/a'a'aimport.png)

效果	

实现	系统需要一个代表宏命令的接口，以定义出具体宏命令所需要的接口。

	

	public interface MacroCommand extends Command {    /\*\*     \* 宏命令聚集的管理方法     \* 可以添加一个成员命令     \*/    public void add\(Command cmd\);    /\*\*     \* 宏命令聚集的管理方法     \* 可以删除一个成员命令     \*/    public void remove\(Command cmd\);}

	

	具体的宏命令MacroAudioCommand类负责把个别的命令合成宏命令。

	

	public class MacroAudioCommand implements MacroCommand {        private List&lt;Command&gt; commandList = new ArrayList&lt;Command&gt;\(\);    /\*\*     \* 宏命令聚集管理方法     \*/    @Override    public void add\(Command cmd\) {        commandList.add\(cmd\);    }    /\*\*     \* 宏命令聚集管理方法     \*/    @Override    public void remove\(Command cmd\) {        commandList.remove\(cmd\);    }    /\*\*     \* 执行方法     \*/    @Override    public void execute\(\) {        for\(Command cmd : commandList\){            cmd.execute\(\);        }    }

	}

	

	客户端类Julia

	

	public class Julia {        public static void main\(String\[\]args\){        //创建接收者对象        AudioPlayer audioPlayer = new AudioPlayer\(\);        //创建命令对象        Command playCommand = new PlayCommand\(audioPlayer\);        Command rewindCommand = new RewindCommand\(audioPlayer\);        Command stopCommand = new StopCommand\(audioPlayer\);                MacroCommand marco = new MacroAudioCommand\(\);                marco.add\(playCommand\);        marco.add\(rewindCommand\);        marco.add\(stopCommand\);        marco.execute\(\);    }}

	

	运行结果如下：

	

	 

	

	来自 &lt;http://www.cnblogs.com/java-my-life/archive/2012/06/01/2526972.html&gt; 

	





