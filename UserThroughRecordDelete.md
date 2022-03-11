# JDBC-Connectivity

package com;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Scanner;

public class BookMenu {

	static Scanner sc;
	static Connection con;
	static Statement st;
	
	public BookMenu() throws ClassNotFoundException, SQLException
	{
		Class.forName("com.mysql.cj.jdbc.Driver");
		
		 con=DriverManager.getConnection("jdbc:mysql://localhost:3306/adjtplus","root","root");
		
		 st=con.createStatement();
		
		 sc=new Scanner(System.in);
	}
	public void delete() throws SQLException
	{
		System.out.println("Enter isbn");
		String isbn=sc.next();
		
		String sql="delete from book where isbn='"+isbn+"'";
	
		st.executeUpdate(sql);
		
		System.out.println("Record Inserted");
	}
	public static void main(String[] args) {
		// TODO Auto-generated method stub

		try
		{
			BookMenu b1=new BookMenu();
			b1.delete();
		}
		catch(ClassNotFoundException | SQLException e)
		{
			e.printStackTrace();
		}
		finally
		{
			try
			{
				st.close();
				con.close();
			}
			catch(SQLException e)
			{
				e.printStackTrace();
			}
		}
	}

}
