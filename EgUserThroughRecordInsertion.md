# JDBC-Connectivity

package com;
import java.sql.*;
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
	public void insert() throws SQLException
	{
		System.out.println("enter isbn");
		String isbn=sc.next();
		System.out.println("Enter book name");
		String bname=sc.next();
		System.out.println("Enter book author");
		String bauthor=sc.next();
		System.out.println("Enter book price");
		double bprice=sc.nextFloat();
		
		String sql="insert into book values('"+isbn+"','"+bname+"','"+bauthor+"','"+bprice+"')";
		
		st.executeUpdate(sql);
		
		System.out.println("Record Inserted");
	}
	public static void main(String[] args) {
		// TODO Auto-generated method stub

		try
		{
			BookMenu b1=new BookMenu();
			b1.insert();
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
