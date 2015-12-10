# work
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.Data.SqlClient;
namespace shiping
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        private void Form1_Load(object sender, EventArgs e)
        {
        }
        private void button2_Click(object sender, EventArgs e)
        {
            string conn = "Server=(local);Integrated Security=True;DataBase=rlsb;"; //定义链接字符串
            string sql = " select ID, personalSex ,carrying from dbo.[DPeS] where 1=1";
            if (sex.Text.Trim() != "")
            { 
                sql += " And personalSex='" + fanhuisex(sex.Text.Trim()) + "'";
            }
             if( comboBox8.Text.Trim () !="")
            {
                sql += " And carrying='" + xiedaiwupin(comboBox8.Text.Trim()) + "'";
            }
             if (comboBox2.Text.Trim() != "")
             {
                 sql += " And footweartype='" + footwear(comboBox2.Text.Trim()) + "'";
             }
             sql += "order by ID";
            SqlConnection connection = new SqlConnection(conn);
            connection.Open();
            SqlDataAdapter sda = new SqlDataAdapter(sql, connection);
            DataTable dt = new DataTable();
            sda.Fill(dt);
            dataGridView1.DataSource = dt;
            //dt.Clear();
            connection.Close();
        }
        public  string fanhuisex(string str)
        {
            if (str == "男人")
            {
                return "personalMale";
            }
            else
            {
                return "personalFemale";
            }
        }
        public string xiedaiwupin(string str)
        {
            if (str =="背包")
            {
                return "carryingBackpack";
            }
            if (str =="邮差包、斜挎包、信差包")
            {
                return "carryingMessengerBag";
            }
            if (str =="手提箱")
            {
                return "carryingSuitcase";
            }
            if (str == "其他")
            {
                return "carryingOther";
            }
            else
            {
                return "carryingNothing";
            }
        }
        public string footwear(string str)
        {
            if (str == "鞋子")
            {
                return "footwearShoes";
            }
            if (str == "运动鞋")
            {
                return "footwearSneaker";
            }
            if (str == "凉鞋")
            {
                return "footwearSandals";
            }
            if (str == "皮鞋")
            {
                return "footwearLeatherShoes";
            }
            if (str == "长筒靴")
            {
                return "footwearStocking";
            }
            else
            {
                return "footwearBoots";
            }
        }
        }
    }
