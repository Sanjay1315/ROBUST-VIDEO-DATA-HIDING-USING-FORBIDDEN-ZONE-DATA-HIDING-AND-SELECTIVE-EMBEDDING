Login using System; using 
System.Collections.Generic; using 
System.ComponentModel; using 
System.Data; using 
System.Drawing; using 
System.Linq; using System.Text; 
using System.Windows.Forms;
namespace Video
{ public partial class Login : 
Form
{ public
Login()
{
InitializeComponent();
}
private void button1_Click(object sender, EventArgs e)
{
if (textBox1.Text == "admin" & textBox2.Text == "admin")
{
mainform m = new mainform(); 
m.Show(); } else {
MessageBox.Show("Invalid Login");
}
}
private void button2_Click(object sender, EventArgs e)
{
Application.Exit();
}
}
}
Main form
using System; using 
System.Collections.Generic; using 
System.ComponentModel; using 
System.Data; using 
System.Drawing; using 
System.Linq; using System.Text; 
using System.Windows.Forms;
namespace Video
{ public partial class mainform : 
Form
{
public mainform()
{
InitializeComponent();
}
private void embedToolStripMenuItem1_Click(object sender, EventArgs e)
{
embed obj = new embed(); 
obj.MdiParent = this;
obj.Show();
}
private void exitToolStripMenuItem_Click(object sender, EventArgs e)
{
Application.Exit();
}
private void extractToolStripMenuItem_Click(object sender, EventArgs e)
{
Extract obj = new Extract(); 
obj.MdiParent = this; obj.Show();
}
private void mainform_FormClosing(object sender, FormClosingEventArgs e)
{
Application.Exit();
}
}
}
EMBEDProcess
using System; using 
System.Collections.Generic; using 
System.ComponentModel; using
System.Data; using 
System.Drawing; using 
System.Text; using 
System.Windows.Forms; using 
System.Data.SqlClient; using 
System.IO;
namespace Video
{ public partial class embed : 
Form
{
SqlConnection cn = new 
SqlConnection("server=.\\sqlexpress;database=RobustVideo;integrated security=true;");
public embed()
{
InitializeComponent();
}
private void button3_Click(object sender, EventArgs e)
{
textBox2.Text = getRandom(1000000, 5000000).ToString();
}
Random r = new Random(); private 
int getRandom(int start, int end)
{
int random = r.Next(start, end); 
return random;
}
string mergeFolder = "";
List<string> Packets = new List<string>(); private 
void button5_Click(object sender, EventArgs e)
{
try
{
FileStream fs = new FileStream(textBox1.Text, FileMode.Open,
FileAccess.Read); int SizeofEachFile = (int) fs.Length; 
byte[] textbytes = GetBytesFromFile(textBox3.Text);
string folderpath = Path.GetDirectoryName(textBox1.Text); string 
baseFileName = Path.GetFileNameWithoutExtension(textBox1.Text); string 
Extension = Path.GetExtension(textBox1.Text);
// FileStream outputFile = new 
FileStream(Path.GetDirectoryName(SourceFile) + "\\" + baseFileName + "." +
FileStream outputFile = new FileStream(folderpath + "\\" + baseFileName
+"_encrypt" + Extension, FileMode.Create, FileAccess.Write); 
mergeFolder = Path.GetDirectoryName(textBox1.Text);
int bytesRead = 0;
byte[] buffer = new byte[SizeofEachFile];
if ((bytesRead = fs.Read(buffer, 0, SizeofEachFile)) > 0)
{
int k=8; for (int j = 0; j <= 
textbytes.Length-1; j++)
{ buffer[k]
= textbytes[j]; k += 8;
}
outputFile.Write(buffer, 0, bytesRead);
//outp.Write(buffer, 0, BytesRead);
string packet = baseFileName + Extension.ToString(); 
Packets.Add(packet);
}
outputFile.Close(); 
fs.Close();
if (cn.State == ConnectionState.Closed) cn.Open();
SqlCommand cmd = new SqlCommand("insert into tbl_encode values('" + 
baseFileName + Extension + "'," + SizeofEachFile + ",'" + textBox2.Text + "','" + textBox3.Text
+ "'," + textbytes.Length + ")", cn); 
cmd.ExecuteNonQuery();
MessageBox.Show("Embed Process Completed Successfully");
}
catch (Exception Ex)
{
throw new ArgumentException(Ex.Message);
}
}
public static byte[] GetBytesFromFile(string fullFilePath)
{
// this method is limited to 2^32 byte files (4.2 GB)
try
FileStream fs = null;
{
fs = File.OpenRead(fullFilePath);
byte[] bytes = new byte[fs.Length];
fs.Read(bytes, 0, Convert.ToInt32(fs.Length)); 
return bytes;
}
finally {
if (fs != null)
{
fs.Close();
fs.Dispose();
}
}
}
clsEmbed obj1; 
Boolean Paused = false;
Boolean Started = false; Boolean PlayedSecond = 
true; private void button1_Click(object sender, 
EventArgs e)
{
if (openFileDialog1.ShowDialog() == DialogResult.OK)
{
obj1.PropAudioFileName = openFileDialog1.FileName; 
textBox1.Text = obj1.PropAudioFileName; button7.Enabled
= true;
}
}
private void button2_Click(object sender, EventArgs e)
{
}
private void embed_Load(object sender, EventArgs e)
{
obj1 = new clsEmbed();
}
private void button7_Click(object sender, EventArgs e)
{ if (textBox1.Text
!= "")
{
PlayedSecond = false;
axVLCPlugin21.playlist.items.clear(); 
axVLCPlugin21.playlist.add(textBox1.Text, "hai", "hai"); 
axVLCPlugin21.playlist.play();
Started = true;
}
}
private void button6_Click(object sender, EventArgs e)
{
axVLCPlugin21.playlist.stop();
}
private void button4_Click(object sender, EventArgs e)
{
openFileDialog2.Title = "Open Text File"; 
openFileDialog2.Filter = "Text Files (*.txt) | *.txt"; if 
(openFileDialog2.ShowDialog() == DialogResult.OK)
{
obj1.PropEmbedTextFileName = 
openFileDialog2.FileName; textBox3.Text = 
obj1.PropEmbedTextFileName; textBox4.Text
= System.IO.File.ReadAllText(textBox3.Text);
}
}
private void btnclose_Click(object sender, EventArgs e)
{
this.Close();
}
}
}