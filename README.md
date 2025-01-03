# Student_Registration_demo2
// Crud in Asp.Net with Add more functionality and file upload.
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Student_Details_Form.aspx.cs" Inherits="EmployeeCRUDWebForms.Student_Details_Form" %>

<script type="text/javascript">
    // JavaScript to clear label on file selection
    document.addEventListener("DOMContentLoaded", function () {
        var fileUpload = document.getElementById('<%= fileUploadImage.ClientID %>');
        var lblFileName = document.getElementById('<%= lblfileName.ClientID %>');

        fileUpload.addEventListener('change', function () {
            if (fileUpload.value) {
                lblFileName.textContent = "";  // Clear label when file is selected
            }
        });
    });
    function PreviewImage(fileUpload) {
        var file = fileUpload.files[0];
        if (file) {
            var reader = new FileReader();
            reader.onload = function (e) {
                var img = document.getElementById('<%= imgPreview.ClientID %>');
                img.src = e.target.result;  // Set image source to uploaded file
            };
            reader.readAsDataURL(file);
            }
        }
</script>
<!DOCTYPE html>
<html>
<head>
    <title>Student Management</title>
</head>
<body>
    <form id="form1" runat="server">
        <h2>Student Personal Details</h2>

        <asp:HiddenField ID="HiddenEmpID" runat="server" />
        First Name:
        <asp:TextBox ID="txtFirstName" runat="server" required></asp:TextBox><br />
        Last Name:
        <asp:TextBox ID="txtLastName" runat="server" required></asp:TextBox><br />
        Email:Id  
        <asp:TextBox ID="txtEmail" runat="server" required></asp:TextBox><br />
        Department:
        <asp:TextBox ID="txtDepartment" runat="server" required></asp:TextBox><br />
        <%--     Gender:  <asp:DropDownList ID="ddlStudentgenders" runat="server" CssClass="form-control">
</asp:DropDownList>--%>
        <asp:ScriptManager ID="ScriptManager1" runat="server" />


        <asp:UpdatePanel ID="UpdatePanel1" runat="server" UpdateMode="Conditional">
            <contenttemplate>
        Gender:  <asp:DropDownList ID="ddlStudentgenders" runat="server" CssClass="form-control">
</asp:DropDownList>

        <asp:Label ID="lblMessage" runat="server" ForeColor="Green"></asp:Label>
    </contenttemplate>
        </asp:UpdatePanel>
        <%@ Register TagPrefix="asp" Namespace="System.Web.UI.WebControls" Assembly="System.Web" %>
        <div id="AFF-Capacitylistdetails">
            <div class="form-group">
                <div class="row">
                    <h2>Student Qualification Details</h2>
                    <div class="col-sm-12" style="overflow: scroll">
                        <table width="100%">
                            <tr>
                                <td>
                                    <asp:GridView ID="GvBlankGrid" runat="server" AllowPaging="False" AutoGenerateColumns="False"
                                        Width="99%" CssClass="table table-bordered" OnRowCommand="GvBlankGrid_RowCommand">
                                        <columns>
<asp:TemplateField HeaderText="qualification" HeaderStyle-HorizontalAlign="Center">
                                                <ItemStyle HorizontalAlign="Center" />
                                                <HeaderStyle HorizontalAlign="Center" />
                                                <ItemTemplate>
                                                    <asp:TextBox ID="txtqname" Width="110px" Text='<%#Eval("qname") %>' runat="server"
                                                         CssClass="form-control" MaxLength="15"></asp:TextBox>
                                                </ItemTemplate>
                                            </asp:TemplateField>

                                            <asp:TemplateField HeaderText="Institute Name" HeaderStyle-HorizontalAlign="Center">
                                                <ItemStyle HorizontalAlign="Center" />
                                                <HeaderStyle HorizontalAlign="Center" />
                                                <ItemTemplate>
                                                    <asp:TextBox ID="txtiname" Width="110px" Text='<%#Eval("iname") %>' runat="server"
                                                         CssClass="form-control" MaxLength="15"></asp:TextBox>
                                                </ItemTemplate>
                                            </asp:TemplateField>
                                                 <asp:TemplateField HeaderText="Marks" HeaderStyle-HorizontalAlign="Center">
                                                <ItemStyle HorizontalAlign="Center" />
                                                <HeaderStyle HorizontalAlign="Center" />
                                                <ItemTemplate>
                                                    <asp:TextBox ID="txtmarks" Width="110px" Text='<%#Eval("marks") %>' runat="server"
                                                         CssClass="form-control" MaxLength="15"></asp:TextBox>
                                                </ItemTemplate>
                                            </asp:TemplateField>
     
                                            <asp:TemplateField HeaderText="Delete">
                                                <ItemTemplate>
                                                  <asp:LinkButton runat="server" ID="lnkDelete" CausesValidation="False"
    AutoUpdateAfterCallBack="True" CommandName="DELETERECROOM" CommandArgument='<%# Container.DataItemIndex %>'
    PreCallBackFunction="btnDelete_PreCallBack">
    <img src="../Images/HardcodedImage.gif" alt="Delete" border="0" />
</asp:LinkButton>
                                                </ItemTemplate>
                                            </asp:TemplateField>
                                        </columns>
                                    </asp:GridView>
                                </td>
                            </tr>

                            <tr>
                                <td align="right">
                                    <asp:Button ID="btnMore" OnClick="btnMore_Click" AutoPostBack="false" runat="server" Text="Add More" CssClass="btn btn-sm btn-warning" />
                                </td>
                            </tr>
                        </table>

                    </div>
                </div>
            </div>
        </div>

        Student Image: 
        <asp:FileUpload ID="fileUploadImage" runat="server" OnChange="PreviewImage(this)" CssClass="form-control" />
        <asp:Label ID="lblfileName" runat="server" ForeColor="Red"></asp:Label>

        <div class="form-group mt-3">
            <asp:Image ID="imgPreview" runat="server" CssClass="img-thumbnail" Width="200" Height="200" />
        </div>
        <div style="text-align: center;">
            <asp:Button ID="btnSave" runat="server" Text="Submit" OnClick="btnSave_Click" CssClass="btn btn-sm btn-warning" />
            <asp:Button ID="btnreset" runat="server" Text="Reset" CssClass="btn btn-sm btn-warning" OnClick="btnreset_Click" />
        </div>
        <br />
        <br />
        <br />
        <div class="table-responsive">
            <asp:GridView ID="gnStudentdetails" runat="server" Width="100%" AllowPaging="True" AutoGenerateColumns="False"
                DataKeyNames="studentid" PageSize="10"
                CssClass="table table-bordered" PagerStyle-CssClass="pagination" OnRowCommand="gnStudentdetails_RowCommand">

                <columns>
            <asp:BoundField DataField="name" HeaderText="Student Name">
                <ItemStyle HorizontalAlign="Left" />
                <HeaderStyle HorizontalAlign="Left" />
            </asp:BoundField>
             <asp:BoundField DataField="email" HeaderText="Email Address">
                <ItemStyle HorizontalAlign="Left" />
                <HeaderStyle HorizontalAlign="Left" />
            </asp:BoundField>
             <asp:BoundField DataField="dept" HeaderText="Department">
                <ItemStyle HorizontalAlign="Left" />
                <HeaderStyle HorizontalAlign="Left" />
            </asp:BoundField>
<asp:TemplateField HeaderText="View Image">
    <ItemTemplate>
        <a href='<%# Eval("filePath") %>' target="_blank">
            <%# Eval("fileName") %>
        </a>
    </ItemTemplate>
</asp:TemplateField>
<asp:TemplateField HeaderText="EDIT">
                <ItemStyle HorizontalAlign="Center" Width="5%" />
                <ItemTemplate>
                    <asp:LinkButton ID="lnkEdit" runat="server" CausesValidation="False" CommandArgument='<%# Eval("studentid") %>'
                        CommandName="EDITREC">
                        <img src="../Images/HardcodedImage.gif" alt="Edit" border="0" />
                    </asp:LinkButton>
                </ItemTemplate>
                <HeaderStyle HorizontalAlign="Center" />
            </asp:TemplateField>
 <asp:TemplateField HeaderText="DELETE">
                <ItemStyle HorizontalAlign="Center" Width="5%" />
                <ItemTemplate>
                    <asp:LinkButton ID="LinkButton1" runat="server" CausesValidation="False" CommandArgument='<%# Eval("studentid") %>'
                        CommandName="DELETESTUDENT" OnClientClick="return confirm('Are you sure you want to delete this record?');">
                       <img src="../Images/HardcodedImage.gif" alt="Delete" border="0" />
                    </asp:LinkButton>
                </ItemTemplate>
                <HeaderStyle HorizontalAlign="Center" />
            </asp:TemplateField>
        </columns>
            </asp:GridView>
        </div>

    </form>
</body>
</html>
----------------------------------------------------------------------------end-------------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.Configuration;
using System.Data;
using System.Data.SqlClient;
using System.IO;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace EmployeeCRUDWebForms
{
    public partial class Student_Details_Form : System.Web.UI.Page
    {
        DataAccess DAobj = new DataAccess();
        protected void Page_Load(object sender, EventArgs e)
        {
            if (!IsPostBack)
            {
                BindDropDown();
                InitializeGrid();
                BindRegistrationGrid();
                string name = fileUploadImage.FileName;
            }
            else
            {

            }
        }
        private void BindDropDown()
        {
            string cs = ConfigurationManager.ConnectionStrings["DBCS"].ConnectionString;
            using (SqlConnection con = new SqlConnection(cs))
            {
                SqlCommand cmd = new SqlCommand("select * from ACD_Employee_gender_mst", con);
                con.Open();
                SqlDataReader reader = cmd.ExecuteReader();
                ddlStudentgenders.DataSource = reader;
                ddlStudentgenders.DataTextField = "GenderName";  // Displayed in the dropdown
                ddlStudentgenders.DataValueField = "Pk_genderid";  // Value behind the scenes
                ddlStudentgenders.DataBind();
                // Optional: Add a default item
                ddlStudentgenders.Items.Insert(0, new ListItem("-- Select Student Gender --", "0"));
            }
        }
        private void BindRegistrationGrid()
        {
            try
            {
                string cs = ConfigurationManager.ConnectionStrings["DBCS"].ConnectionString;
                using (SqlConnection con = new SqlConnection(cs))
                {
                    string spName = "Get_StudentDetails";
                    SqlCommand cmd = new SqlCommand(spName, con);
                    cmd.CommandType = CommandType.StoredProcedure;
                    SqlDataAdapter da = new SqlDataAdapter(cmd);
                    DataSet ds = new DataSet();
                    con.Open();
                    da.Fill(ds);
                    gnStudentdetails.DataSource = ds.Tables[0];
                    gnStudentdetails.DataBind();
                    con.Close();
                }
            }
            catch (Exception ex)
            {
            }
        }
        private void InitializeGrid()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("qname", typeof(string));
            dt.Columns.Add("iname", typeof(string));
            dt.Columns.Add("marks", typeof(string));
            // Add an empty row initially
            DataRow dr = dt.NewRow();
            dt.Rows.Add(dr);
            GvBlankGrid.DataSource = dt;
            GvBlankGrid.DataBind();
            ViewState["dtl"] = dt;
        }
        protected void btnSave_Click(object sender, EventArgs e)
        {
            if (btnSave.Text == "Submit")
            {
                Save();
                BindRegistrationGrid();
                Clear();
            }
            else
            {
                Update();
                BindRegistrationGrid();
                Clear();
            }
        }
        protected void ClientMessaging(string msg)
        {
            string script = $"alert('{msg}');";
            ScriptManager.RegisterStartupScript(this, this.GetType(), "errMsg", script, true);
        }
        protected DataTable GetXML()
        {
            // 1. Get File Details
            string fileName = Path.GetFileName(fileUploadImage.PostedFile.FileName);
            //string filePath = @"D:\AIIA\UploadedImages\" + fileName;
            //string filePath = @"~/UploadedImages/" + fileName;
            //string serverPath = Server.MapPath(filePath);
            //imgPreview.ImageUrl = ResolveUrl("~/UploadedImages/" + lblfileName.Text);

            // 2. Save to Folder
            // fileUploadImage.SaveAs(filePath);
            string filePath = "~/UploadedImages/" + fileName;
            string serverPath = Server.MapPath(filePath);  // Convert to physical path
            fileUploadImage.SaveAs(serverPath);

            DataTable dt = new DataTable("Student");
            // Define columns manually
            dt.Columns.Add("fname", typeof(string));
            dt.Columns.Add("lname", typeof(string));
            dt.Columns.Add("email", typeof(string));
            dt.Columns.Add("dept", typeof(string));
            dt.Columns.Add("Fk_genderid", typeof(int));
            dt.Columns.Add("fileName", typeof(string));
            dt.Columns.Add("filePath", typeof(string));

            // Create a new DataRow and add values from TextBoxes
            DataRow dr = dt.NewRow();
            dr["fname"] = txtFirstName.Text.Trim();
            dr["lname"] = txtLastName.Text.Trim();
            dr["email"] = txtEmail.Text.Trim();
            dr["dept"] = txtDepartment.Text.Trim();
            dr["Fk_genderid"] = ddlStudentgenders.SelectedValue;
            dr["fileName"] = fileName;
            dr["filePath"] = filePath;

            // Add row to the DataTable
            dt.Rows.Add(dr);

            //return ds;
            return dt;
        }
        protected DataTable GetXMLforupdate()
        {
            // 1. Get File Details
            //string fileName = Path.GetFileName(fileUploadImage.PostedFile.FileName);
            //string filePath = @"D:\AIIA\UploadedImages\" + fileName;
            //string filePath = @"~/UploadedImages/" + fileName;
            //string serverPath = Server.MapPath(filePath);
            //imgPreview.ImageUrl = ResolveUrl("~/UploadedImages/" + lblfileName.Text);

            // 2. Save to Folder
            // fileUploadImage.SaveAs(filePath);
            //string filePath = "~/UploadedImages/" + fileName;
            //string serverPath = Server.MapPath(filePath);  // Convert to physical path
            //fileUploadImage.SaveAs(serverPath);

            DataTable dt = new DataTable("Student");
            // Define columns manually
            dt.Columns.Add("fname", typeof(string));
            dt.Columns.Add("lname", typeof(string));
            dt.Columns.Add("email", typeof(string));
            dt.Columns.Add("dept", typeof(string));
            dt.Columns.Add("Fk_genderid", typeof(int));
            //dt.Columns.Add("fileName", typeof(string));
            //dt.Columns.Add("filePath", typeof(string));

            // Create a new DataRow and add values from TextBoxes
            DataRow dr = dt.NewRow();
            dr["fname"] = txtFirstName.Text.Trim();
            dr["lname"] = txtLastName.Text.Trim();
            dr["email"] = txtEmail.Text.Trim();
            dr["dept"] = txtDepartment.Text.Trim();
            dr["Fk_genderid"] = ddlStudentgenders.SelectedValue;
            //dr["fileName"] = fileName;
            //dr["filePath"] = filePath;

            // Add row to the DataTable
            dt.Rows.Add(dr);

            //return ds;
            return dt;
        }
        protected DataTable AddDynamicValue()
        {
            DataTable dt = new DataTable("Student_Qualification_dtl");

            // Define columns manually
            dt.Columns.Add("qname", typeof(string));
            dt.Columns.Add("iname", typeof(string));
            dt.Columns.Add("marks", typeof(string));
            DataRow dr;
            // Loop through GridView rows and populate DataTable
            for (int i = 0; i < GvBlankGrid.Rows.Count; i++)
            {
                dr = dt.NewRow();
                // Find TextBoxes within the GridView rows
                string qname = ((TextBox)GvBlankGrid.Rows[i].FindControl("txtqname")).Text;
                string iname = ((TextBox)GvBlankGrid.Rows[i].FindControl("txtiname")).Text;
                string marks = ((TextBox)GvBlankGrid.Rows[i].FindControl("txtmarks")).Text;

                // Add values to the DataRow
                dr["qname"] = qname.Trim();
                dr["iname"] = iname.Trim();
                dr["marks"] = marks.Trim();

                // Add the row to the DataTable
                dt.Rows.Add(dr);
            }
            //return ds;
            return dt;
        }
        private string GenerateXml()
        {
            DataSet dsMain = new DataSet();
            DataTable tbl1 = GetXML();
            DataTable tbl2 = AddDynamicValue();
            dsMain.Merge(tbl1);
            dsMain.Merge(tbl2);
            string xmlDoc = dsMain.GetXml();
            return xmlDoc;
        }
        private string GenerateXmlforupdate()
        {
            DataSet dsMain = new DataSet();
            DataTable tbl1;
            if (fileUploadImage.HasFile)
            {
                 tbl1 = GetXML();

            }
            else
            {
                 tbl1 = GetXMLforupdate();
            }
            DataTable tbl2 = AddDynamicValue();
            dsMain.Merge(tbl1);
            dsMain.Merge(tbl2);
            string xmlDoc = dsMain.GetXml();
            return xmlDoc;
        }
        private void Save()
        {
            try
            {
                string xmlDoc = GenerateXml();
                string cs = ConfigurationManager.ConnectionStrings["DBCS"].ConnectionString;
                SqlConnection con = new SqlConnection(cs);
                string spName = "ACD_StudentRegistrationInsert";
                SqlCommand cmd = new SqlCommand(spName, con);
                cmd.CommandType = CommandType.StoredProcedure;
                con.Open();
                cmd.Parameters.AddWithValue("@xmlDoc", xmlDoc);
                if (cmd.ExecuteNonQuery() > 0)
                {
                    ClientMessaging("Data Saved Succeessfully");
                }
                else
                {
                    ClientMessaging("Duplicate Data Found");
                }
                con.Close();
            }
            catch (Exception ex)
            {
            }
        }
        private void Clear()
        {
            txtFirstName.Text = "";
            txtLastName.Text = "";
            txtEmail.Text = "";
            txtDepartment.Text = "";
            ddlStudentgenders.SelectedValue = 0.ToString();
            InitializeGrid();
        }
        private void DeleteImage()
        {
            try
            {
                string cs = ConfigurationManager.ConnectionStrings["DBCS"].ConnectionString;
                using (SqlConnection con = new SqlConnection(cs))
                {
                    int index = Convert.ToInt32(ViewState["editid"]);
                    string spName = "ACD_Studentbyid";
                    SqlCommand cmd = new SqlCommand(spName, con);
                    cmd.CommandType = CommandType.StoredProcedure;
                    SqlDataAdapter da = new SqlDataAdapter(cmd);
                    cmd.Parameters.AddWithValue("@studentid", index);
                    DataSet ds = new DataSet();
                    con.Open();
                    da.Fill(ds);
                    lblfileName.Text = ds.Tables[0].Rows[0]["fileName"].ToString();
                    string folderPath = ds.Tables[0].Rows[0]["filePath"].ToString();
                    string oldFileName = lblfileName.Text;
                    if (fileUploadImage.HasFile)
                    {
                        if (!string.IsNullOrEmpty(folderPath))
                        {
                            // Construct full file path
                            //string oldFilePath = Path.Combine(folderPath, oldFileName);
                            string serverPath = Server.MapPath(folderPath);  // Convert to physical path
                            if (File.Exists(serverPath))  // Check for file, not folder
                            {
                                File.Delete(serverPath);  // Delete old file
                            }
                        }
                    }

                }
            }
            catch (Exception ex)
            {


            }
        }
        private void Update()
        {
            try
            {
                lblfileName.Text = "";
                DeleteImage();
                lblfileName.Text = "";
                int updateid = Convert.ToInt32(ViewState["editid"]);
                string xmlDoc = GenerateXmlforupdate();
                string cs = ConfigurationManager.ConnectionStrings["DBCS"].ConnectionString;
                SqlConnection con = new SqlConnection(cs);
                string spName;
                if
                      (fileUploadImage.HasFile)
                    {
                        spName = "ACD_StudentReg_update";
                    }
                    else {
                        spName = "ACD_StudentReg_update1";
                    }

                SqlCommand cmd = new SqlCommand(spName, con);
                cmd.CommandType = CommandType.StoredProcedure;
                con.Open();
                cmd.Parameters.AddWithValue("@xmlDoc", xmlDoc);
                cmd.Parameters.AddWithValue("@Pk_studid", updateid);
                cmd.ExecuteNonQuery();
                con.Close();
                ClientMessaging("Record Update Successfully");
            }
            catch (Exception ex)
            {
            }
        }
        protected void GvBlankGrid_RowCommand(object sender, GridViewCommandEventArgs e)
        {
            if (e.CommandName == "DELETERECROOM")
            {
                int rowIndex = Convert.ToInt32(e.CommandArgument);
                DataTable dt = ViewState["dtl"] as DataTable;

                if (dt != null && dt.Rows.Count > 1)
                {
                    dt.Rows[rowIndex].Delete();
                    dt.AcceptChanges();

                    GvBlankGrid.DataSource = dt;
                    GvBlankGrid.DataBind();

                    ViewState["dtl"] = dt;
                }
                else
                {
                    // Prevent deleting the last row
                    ScriptManager.RegisterStartupScript(this, GetType(), "alert", "alert('Cannot delete the last row.');", true);
                }

            }
        }
        protected void btnMore_Click(object sender, EventArgs e)
        {
            try
            {
                DataTable dt = ViewState["dtl"] as DataTable;

                // Save existing rows
                for (int i = 0; i < GvBlankGrid.Rows.Count; i++)
                {
                    TextBox qname = (TextBox)GvBlankGrid.Rows[i].FindControl("txtqname");
                    TextBox iname = (TextBox)GvBlankGrid.Rows[i].FindControl("txtiname");
                    TextBox marks = (TextBox)GvBlankGrid.Rows[i].FindControl("txtmarks");
                    DataRow dr = dt.Rows[i];
                    dr["qname"] = qname.Text;
                    dr["iname"] = iname.Text;
                    dr["marks"] = marks.Text;
                }
                // Add a new blank row
                DataRow newRow = dt.NewRow();
                dt.Rows.Add(newRow);
                GvBlankGrid.DataSource = dt;
                GvBlankGrid.DataBind();
                ViewState["dtl"] = dt;
            }
            catch (Exception ex)
            {
                // Handle errors
                Response.Write("Error: " + ex.Message);
            }
        }
        protected void gnStudentdetails_RowCommand(object sender, GridViewCommandEventArgs e)
        {
            try
            {
                if (e.CommandName == "DELETESTUDENT")
                {
                    int index = Convert.ToInt32(e.CommandArgument);
                    string cs = ConfigurationManager.ConnectionStrings["DBCS"].ConnectionString;
                    SqlConnection con = new SqlConnection(cs);
                    string spName = "ACD_deleteStudents";
                    SqlCommand cmd = new SqlCommand(spName, con);
                    cmd.CommandType = CommandType.StoredProcedure;
                    con.Open();
                    cmd.Parameters.AddWithValue("@studentid", index);
                    cmd.ExecuteNonQuery();
                    con.Close();
                    BindRegistrationGrid();
                    Clear();
                }
                else
                {
                    btnSave.Text = "Update";
                    string cs = ConfigurationManager.ConnectionStrings["DBCS"].ConnectionString;
                    using (SqlConnection con = new SqlConnection(cs))
                    {
                        int index = Convert.ToInt32(e.CommandArgument);
                        ViewState["editid"] = Convert.ToInt32(e.CommandArgument);
                        string spName = "ACD_Studentbyid";
                        SqlCommand cmd = new SqlCommand(spName, con);
                        cmd.CommandType = CommandType.StoredProcedure;
                        SqlDataAdapter da = new SqlDataAdapter(cmd);
                        cmd.Parameters.AddWithValue("@studentid", index);
                        DataSet ds = new DataSet();
                        con.Open();
                        da.Fill(ds);
                        txtFirstName.Text = ds.Tables[0].Rows[0]["fname"].ToString();
                        txtLastName.Text = ds.Tables[0].Rows[0]["lname"].ToString();
                        txtEmail.Text = ds.Tables[0].Rows[0]["email"].ToString();
                        txtDepartment.Text = ds.Tables[0].Rows[0]["dept"].ToString();
                        ddlStudentgenders.SelectedValue= ds.Tables[0].Rows[0]["Fk_genderid"].ToString();
                        lblfileName.Text = ds.Tables[0].Rows[0]["fileName"].ToString();

                        imgPreview.ImageUrl = ResolveUrl("~/UploadedImages/" + lblfileName.Text);
                        GvBlankGrid.DataSource = ds.Tables[1];
                        GvBlankGrid.DataBind();
                        DataTable dt = ds.Tables[1];

                        // Save existing rows
                        for (int i = 0; i < GvBlankGrid.Rows.Count; i++)
                        {

                            TextBox qname = (TextBox)GvBlankGrid.Rows[i].FindControl("txtqname");
                            TextBox iname = (TextBox)GvBlankGrid.Rows[i].FindControl("txtiname");
                            TextBox marks = (TextBox)GvBlankGrid.Rows[i].FindControl("txtmarks");
                            DataRow dr = dt.Rows[i];
                            dr["qname"] = qname.Text;
                            dr["iname"] = iname.Text;
                            dr["marks"] = marks.Text;
                        }
                        GvBlankGrid.DataSource = dt;
                        GvBlankGrid.DataBind();

                        ViewState["dtl"] = dt;
                    }

                }
            }
            catch (Exception ex)
            {
            }
        }
        protected void btnreset_Click(object sender, EventArgs e)
        {
            Clear();
        }
    }
    internal class DataAccess
    {
    }
}
--------------------------------------------------------------------end---------------------------------------------------------------------
CREATE PROCEDURE ACD_StudentRegistrationInsert                                                         
(                                                     
    @xmlDoc VARCHAR(MAX)                                                       
)                                                             
AS               
BEGIN                                                                                                         
    DECLARE @ERR INT, @Idoc INT, @fk_stid INT, @Result INT                                                                                                                  
    SET @ERR = 0                                                                                                               
      
    BEGIN                                                                                                         
        -- Parse XML document        
        EXEC sp_xml_preparedocument @Idoc OUTPUT, @xmlDoc                                                               
        SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;                                                    
                
        BEGIN TRY                                                                                                          
            BEGIN TRAN              
      
            -- Check for duplicate email      
            IF EXISTS (      
                SELECT 1       
                FROM Student_registraion_Mst      
                WHERE email IN (      
                    SELECT email FROM OPENXML(@Idoc, 'NewDataSet/Student', 2)      
                    WITH (email VARCHAR(100))      
                )      
            )      
            BEGIN      
                -- Duplicate found, return without insertion      
                SELECT 'Duplicate record exists' AS msg, 0 AS success;      
                ROLLBACK TRAN;      
                RETURN;      
            END      
      
            -- Insert data into Student_registraion_Mst        
            INSERT INTO Student_registraion_Mst(fname, lname, email, dept,Fk_genderid,fileName,filePath)                   
            SELECT fname, lname, email, dept, Fk_genderid,fileName,filePath                    
            FROM OPENXML(@Idoc, 'NewDataSet/Student', 2)                               
            WITH (fname VARCHAR(100), lname VARCHAR(100), email VARCHAR(100), dept VARCHAR(100),Fk_genderid int,  
   fileName VARCHAR(500),    
   filePath VARCHAR(500));                              
                   
            -- Capture newly inserted student ID        
            SET @fk_stid = SCOPE_IDENTITY();            
        
            -- Insert data into Student_Qualification_dtl        
            INSERT INTO Student_Qualification_dtl(fk_studentid, qname, Iname, marks)                          
            SELECT @fk_stid, qname, iname, marks                          
            FROM OPENXML(@Idoc, 'NewDataSet/Student_Qualification_dtl', 2)                             
            WITH (qname VARCHAR(100), iname VARCHAR(100), marks VARCHAR(100));                            
      
            -- Commit transaction if no errors        
            COMMIT TRAN;        
            SELECT 'Data Inserted Successfully' AS msg, 1 AS success;        
                    
        END TRY        
        BEGIN CATCH                                                              
            IF @@TRANCOUNT > 0                                                              
                ROLLBACK TRAN;                                                             
        
            DECLARE                                                              
                @ErrMsg NVARCHAR(4000),                                                               
                @ErrSeverity INT;                                                                
        
            SELECT         
                @ErrMsg = ERROR_MESSAGE(),                                                             
                @ErrSeverity = ERROR_SEVERITY();                                                             
        
            -- Return error message        
            SELECT @ErrMsg AS msg, 0 AS success;                                                              
            RAISERROR(@ErrMsg, @ErrSeverity, 1);                                                             
        END CATCH;                                   
        
        -- Clean up XML parser        
        EXEC sp_xml_removedocument @Idoc;          
    END                                                                   
END 
------------------------------------------------------------end--------------------------------------------------------------------------------
/*            
Created By: Sonu sharma           
Created Date: 26/7/2023            
Module: New Pre Examination            
Call From: Exam_Centre_Mst            
Purpose: Update Data When we want to change Exam Center Detail & Room Capacity            
*/            
           
                                
CREATE PROCEDURE ACD_StudentReg_update                                           
(                  
            
@xmlDoc varchar(max),            
@Pk_studid int            
)                                                    
AS         
        
--Declare @xmlDoc varchar(max)='<NewDataSet>        
--  <Exam_PreExamCenter_Mst>        
--    <Pk_PreExamId>0</Pk_PreExamId>        
--    <ExamCenterCode>ABC_898</ExamCenterCode>        
--    <ExamCenterId>1</ExamCenterId>        
--    <ExamCenterAddress>New Delhi NCR</ExamCenterAddress>        
--    <ContactDetails>9685885888</ContactDetails>        
--    <ContactMail>Amit87KJ@gmail.com</ContactMail>        
--    <ContactDetailsName>AMIT</ContactDetailsName>        
--    <FK_CityId>1436</FK_CityId>        
--    <CenterSeatCapacity>500</CenterSeatCapacity>        
--    <IsActive>true</IsActive>        
--    <FK_GeoLocationId>1299</FK_GeoLocationId>        
--    <fk_examconfigid>1</fk_examconfigid>        
--  </Exam_PreExamCenter_Mst>        
--  <Exam_CapacityRoom_Mst>        
--    <Pk_SeatCapacityCenter>0</Pk_SeatCapacityCenter>        
--    <Fk_RoomCenterId>1</Fk_RoomCenterId>        
--    <PriorityOrder>1</PriorityOrder>        
--    <CapacityAtRoom>150</CapacityAtRoom>        
--  </Exam_CapacityRoom_Mst>        
--  <Exam_CapacityRoom_Mst>        
--    <Pk_SeatCapacityCenter>1</Pk_SeatCapacityCenter>        
--    <Fk_RoomCenterId>2</Fk_RoomCenterId>        
--    <PriorityOrder>2</PriorityOrder>        
--    <CapacityAtRoom>250</CapacityAtRoom>        
--  </Exam_CapacityRoom_Mst>        
--  <Exam_CapacityRoom_Mst>        
--    <Pk_SeatCapacityCenter>2</Pk_SeatCapacityCenter>        
--    <Fk_RoomCenterId>3</Fk_RoomCenterId>        
--    <PriorityOrder>3</PriorityOrder>        
--    <CapacityAtRoom>200</CapacityAtRoom>        
--  </Exam_CapacityRoom_Mst>        
--</NewDataSet>',            
--@Pk_PreExamId int=28            
                                          
  DECLARE @ERR Int                                                                                            
  DECLARE @Idoc int                                                                                                                   
                                                                                                                           
SET @ERR = 0                                                                                                      
BEGIN                                                                                                 
EXEC sp_xml_preparedocument @Idoc OUTPUT, @xmlDoc                                                     
--SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;                                            
BEGIN TRY                                                                                                  
BEGIN TRAN                                                  
      
   Update Student_registraion_Mst Set fname=X.fname, lname=X.lname, email=X.email,              
   dept=X.dept,Fk_genderid=X.Fk_genderid,fileName =X.fileName ,  filePath =X.filePath          
   FROM OPENXML(@Idoc,'NewDataSet/Student',2)                       
   With(fname varchar(100),lname varchar(100),email varchar(100),          
   dept varchar(100),Fk_genderid int,fileName varchar(500),filePath varchar(500))X              
   Where Student_registraion_Mst.studentid=@Pk_studid            
            
   Delete From Student_Qualification_dtl Where fk_studentid=@Pk_studid            
            
   Insert Into Student_Qualification_dtl(fk_studentid,qname,Iname,marks)                  
   Select @Pk_studid,qname, iname,marks                 
   FROM OPENXML(@Idoc,'NewDataSet/Student_Qualification_dtl',2)                   
   With(fk_studentid int,qname varchar(100),iname varchar(100),marks varchar(100))         
     
  COMMIT TRAN                                                
                                                                                                  
END TRY                                                    
BEGIN CATCH                                                 
IF @@TranCount > 0                                                      
ROLLBACK                                                      
DECLARE                                                      
@ErrMsg      NVARCHAR(4000),                                                      
@ErrSeverity INT;                                                      
SELECT @ErrMsg = ERROR_MESSAGE(),                                                    
 @ErrSeverity = ERROR_SEVERITY()                                                    
 select @ErrMsg msg, 0 success                                                     
 RAISERROR(@ErrMsg, @ErrSeverity, 1)                                                    
END CATCH                                                    
END 
------------------------------------------------------------------end----------------------------------------------------------------------
/*              
Created By: Sonu sharma             
Created Date: 26/7/2023              
Module: New Pre Examination              
Call From: Exam_Centre_Mst              
Purpose: Update Data When we want to change Exam Center Detail & Room Capacity              
*/              
             
                                  
CREATE PROCEDURE ACD_StudentReg_update1                                             
(                    
              
@xmlDoc varchar(max),              
@Pk_studid int              
)                                                      
AS           
          
--Declare @xmlDoc varchar(max)='<NewDataSet>          
--  <Exam_PreExamCenter_Mst>          
--    <Pk_PreExamId>0</Pk_PreExamId>          
--    <ExamCenterCode>ABC_898</ExamCenterCode>          
--    <ExamCenterId>1</ExamCenterId>          
--    <ExamCenterAddress>New Delhi NCR</ExamCenterAddress>          
--    <ContactDetails>9685885888</ContactDetails>          
--    <ContactMail>Amit87KJ@gmail.com</ContactMail>          
--    <ContactDetailsName>AMIT</ContactDetailsName>          
--    <FK_CityId>1436</FK_CityId>          
--    <CenterSeatCapacity>500</CenterSeatCapacity>          
--    <IsActive>true</IsActive>          
--    <FK_GeoLocationId>1299</FK_GeoLocationId>          
--    <fk_examconfigid>1</fk_examconfigid>          
--  </Exam_PreExamCenter_Mst>          
--  <Exam_CapacityRoom_Mst>          
--    <Pk_SeatCapacityCenter>0</Pk_SeatCapacityCenter>          
--    <Fk_RoomCenterId>1</Fk_RoomCenterId>          
--    <PriorityOrder>1</PriorityOrder>          
--    <CapacityAtRoom>150</CapacityAtRoom>          
--  </Exam_CapacityRoom_Mst>          
--  <Exam_CapacityRoom_Mst>          
--    <Pk_SeatCapacityCenter>1</Pk_SeatCapacityCenter>          
--    <Fk_RoomCenterId>2</Fk_RoomCenterId>          
--    <PriorityOrder>2</PriorityOrder>          
--    <CapacityAtRoom>250</CapacityAtRoom>          
--  </Exam_CapacityRoom_Mst>          
--  <Exam_CapacityRoom_Mst>          
--    <Pk_SeatCapacityCenter>2</Pk_SeatCapacityCenter>          
--    <Fk_RoomCenterId>3</Fk_RoomCenterId>          
--    <PriorityOrder>3</PriorityOrder>          
--    <CapacityAtRoom>200</CapacityAtRoom>          
--  </Exam_CapacityRoom_Mst>          
--</NewDataSet>',              
--@Pk_PreExamId int=28              
                                            
  DECLARE @ERR Int                                                                                              
  DECLARE @Idoc int                                                                                                                     
                                                                                                                             
SET @ERR = 0                                                                                                        
BEGIN                                                                                                   
EXEC sp_xml_preparedocument @Idoc OUTPUT, @xmlDoc                                                       
--SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;                                              
BEGIN TRY                                                                                                    
BEGIN TRAN                                                    
         
   Update Student_registraion_Mst Set fname=X.fname, lname=X.lname, email=X.email,                
   dept=X.dept,Fk_genderid=X.Fk_genderid           
   FROM OPENXML(@Idoc,'NewDataSet/Student',2)                         
   With(fname varchar(100),lname varchar(100),email varchar(100),            
   dept varchar(100),Fk_genderid int)X                
   Where Student_registraion_Mst.studentid=@Pk_studid              
              
   Delete From Student_Qualification_dtl Where fk_studentid=@Pk_studid              
              
   Insert Into Student_Qualification_dtl(fk_studentid,qname,Iname,marks)                    
  Select @Pk_studid,qname, iname,marks                   
   FROM OPENXML(@Idoc,'NewDataSet/Student_Qualification_dtl',2)                     
   With(fk_studentid int,qname varchar(100),iname varchar(100),marks varchar(100))           
      
  COMMIT TRAN                                                  
                                                    
                                                    
END TRY                                                      
BEGIN CATCH                                                   
IF @@TranCount > 0                                                        
ROLLBACK                                                        
DECLARE                                                        
@ErrMsg      NVARCHAR(4000),                                                        
@ErrSeverity INT;                                                        
SELECT @ErrMsg = ERROR_MESSAGE(),                                                      
 @ErrSeverity = ERROR_SEVERITY()                                                      
 select @ErrMsg msg, 0 success                                                       
 RAISERROR(@ErrMsg, @ErrSeverity, 1)                                                      
END CATCH                                                      
END 
------------------------------------------------------------------end--------------------------------------------------------------------
create proc ACD_Studentbyid  
@studentid int  
as  
begin   
select *  from Student_registraion_Mst where studentid=@studentid  
select * from  Student_Qualification_dtl where fk_studentid= @studentid  
  
end
----------------------------------------------------------------end----------------------------------------------------------------------
CREATE proc Get_StudentDetails    
as    
begin     
--select studentid,fname+' '+lname as name,email,dept,filePath from Student_registraion_Mst    
SELECT studentid,  
       fname + ' ' + lname AS name,  
       email,  
       dept,fileName,  
       REPLACE(filePath, '~', '') AS filePath  
FROM Student_registraion_Mst;  
  
    
end 
--------------------------------------------------------------end-----------------------------------------------------------------------





