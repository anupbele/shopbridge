# shopbridge
"ShopBridge" is an e-commerce application.
//ASP.NET CODE
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
    <style type="text/css">
        .style1
        {
            height: 114px;
        }
        .style2
        {
            height: 89px;
            width: 506px;
        }
        .style3
        {
            height: 89px;
            width: 173px;
        }
        .style4
        {
            width: 173px;
        }
        .style5
        {
            height: 89px;
            width: 35px;
        }
        .style6
        {
            width: 35px;
        }
        .style7
        {
            width: 506px;
        }
    </style>
</head>
<body>
    <form id="form1" runat="server">
    <div>

    <table style="width: 52%; height: 546px;" align="center">
        <tr>
            <td align="center" bgcolor="#FFFF99" class="style1" colspan="3" 
                style="font-size: xx-large; color: #0000CC">
                &nbsp;
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 
                ShopBridge&nbsp;
            </td>
        </tr>
        <tr>
            <td class="style3">
                ITEM NAME</td>
            <td class="style2">
                &nbsp;
                <asp:TextBox ID="TextBox1" runat="server" Height="27px" Width="267px"></asp:TextBox>
            </td>
            <td class="style5">
                &nbsp;
                <asp:RequiredFieldValidator ID="RequiredFieldValidator1" runat="server" 
                    ControlToValidate="TextBox1" ErrorMessage="ENTER ITEM" ForeColor="#FF0066"></asp:RequiredFieldValidator>
            </td>
        </tr>
        <tr>
            <td class="style3">
                DESCRIPTION</td>
            <td class="style2">
                <asp:TextBox ID="TextBox2" runat="server" TextMode="MultiLine" Height="88px" 
                    Width="317px"></asp:TextBox>
            </td>
            <td class="style5">
                <asp:RequiredFieldValidator ID="RequiredFieldValidator2" runat="server" 
                    ControlToValidate="TextBox2" ErrorMessage="DESCRIPTION" 
                    ForeColor="#FF0066"></asp:RequiredFieldValidator>
            </td>
        </tr>
        <tr>
            <td class="style4">
                &nbsp;
                QUANTITY 
            </td>
            <td class="style7">
                &nbsp;<asp:TextBox ID="TextBox3" runat="server" Height="40px" Width="139px"></asp:TextBox>
            </td>
            <td class="style6">
                <asp:RequiredFieldValidator ID="RequiredFieldValidator3" runat="server" 
                    ControlToValidate="TextBox3" ErrorMessage="QUANTITY" ForeColor="#FF0066"></asp:RequiredFieldValidator>
            </td>
        </tr>
        <tr>
            <td class="style4">
                PRICE</td>
            <td class="style7">
                <asp:TextBox ID="TextBox4" runat="server"></asp:TextBox>
            </td>
            <td class="style6">
                &nbsp;</td>
        </tr>
        <tr>
            <td class="style4">
                &nbsp;</td>
            <td class="style7">
                <asp:Button ID="Button1" runat="server" Height="46px" Text="ADDITEM" 
                    Width="115px" ForeColor="#000099" onclick="Button1_Click" />
                <asp:Button ID="Button2" runat="server" Height="46px" Text="MODIFY" 
                    Width="122px" ForeColor="#0000CC" onclick="Button2_Click" />
                <asp:Button ID="Button3" runat="server" Height="46px" Text="DELETE" 
                    Width="122px" ForeColor="#000099" onclick="Button3_Click" />
                <asp:Button ID="Button4" runat="server" Height="46px" Text="LIST" 
                    Width="122px" ForeColor="#0000CC" onclick="Button4_Click" />
            </td>
            <td class="style6">
                <asp:Label ID="Label1" runat="server" Text="Label"></asp:Label>
            </td>
        </tr>
    </table>
    </div>
    <div>
        <asp:GridView ID="GridView1" runat="server" AutoGenerateColumns="False" 
            DataSourceID="SqlDataSource1">
            <Columns>
                <asp:BoundField DataField="ITNAME" HeaderText="ITNAME" 
                    SortExpression="ITNAME" />
                <asp:BoundField DataField="DESCRIPTION" HeaderText="DESCRIPTION" 
                    SortExpression="DESCRIPTION" />
                <asp:BoundField DataField="QTY" HeaderText="QTY" SortExpression="QTY" />
                <asp:BoundField DataField="PRICE" HeaderText="PRICE" SortExpression="PRICE" />
            </Columns>
        </asp:GridView>
        <asp:SqlDataSource ID="SqlDataSource1" runat="server" 
            ConnectionString="<%$ ConnectionStrings:SHOPBRIDGEConnectionString %>" 
            SelectCommand="SELECT [ITNAME], [DESCRIPTION], [QTY], [PRICE] FROM [INVENTRY]">
        </asp:SqlDataSource>
    </div>
    
    </form>
</body>
</html>


//C# CODE
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Data.SqlClient;

public partial class _Default : System.Web.UI.Page
{
    SqlConnection con = null;

   
    protected void Page_Load(object sender, EventArgs e)
    {
        con = new SqlConnection("Data Source=.\\SQLEXPRESS;AttachDbFilename=c:\\ShopBridge\\SHOPBRIDGE.MDF;Integrated Security=True;User Instance=True");

       
    }
    protected void Button1_Click(object sender, EventArgs e)
    {
        con.Open();

        SqlCommand cmd = new SqlCommand("insert into INVENTRY values('" + TextBox1.Text + "','" + TextBox2.Text + "','" + TextBox3.Text + "','" + TextBox4.Text + "')", con);
        int result = cmd.ExecuteNonQuery();
        if (result > 0)
        {

            Label1.Text = " INSERT INVENTRY";
            
        }
        else
        {

            Label1.Text = "  NO ITEM";
        }
    
    }
    protected void Button2_Click(object sender, EventArgs e)
    {
        con.Open();
        string updtcmd = "update  INVENTRY set ITNAME='" + TextBox1.Text + "'";
       SqlCommand cmd = new SqlCommand(updtcmd, con);

        cmd.ExecuteNonQuery();
        Label1.Text = "Record Updated Successfully!!";
        


    }
    protected void Button3_Click(object sender, EventArgs e)
    {
        con.Open();

        string del = "delete from INVENTRY where ITNAME='" + TextBox1.Text + "'";
        SqlCommand cmd = new SqlCommand(del, con);

          cmd.ExecuteNonQuery();
     
        

            Label1.Text = " delete INVENTRY";

        


    }
    protected void Button4_Click(object sender, EventArgs e)
    {

    }
}



