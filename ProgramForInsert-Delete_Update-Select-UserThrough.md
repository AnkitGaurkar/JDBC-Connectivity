# JDBC-Connectivity

package com;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Scanner;

public class BookMenu {

	static Scanner sc;
	static Connection con;
	static Statement st;
	//private static Object exit;
	
	public BookMenu() throws ClassNotFoundException, SQLException
	{
		Class.forName("com.mysql.cj.jdbc.Driver");
		
		 con=DriverManager.getConnection("jdbc:mysql://localhost:3306/adjtplus","root","root");
		
		 st=con.createStatement();
		
		 sc=new Scanner(System.in);
	}
	public void insert() throws SQLException
	{
		System.out.println("Enter isbn");
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
	
	public void delete() throws SQLException
	{
		System.out.println("Enter isbn");
		String isbn=sc.next();
		
		String sql="delete from book where isbn='"+isbn+"' ";
		
		st.executeUpdate(sql);
		
		System.out.println("Record Deleted");
	}
	
	public void update() throws SQLException
	{
		System.out.println("Enter isbn");
		String isbn=sc.next();
		System.out.println("Enter bname");
		String bname=sc.next();
		System.out.println("Enter bauthor");
		String bauthor=sc.next();
		System.out.println("Enter bprice");
		double bprice=sc.nextFloat();
		
		String sql ="update book set bname='"+bname+"', bauthor='"+bauthor+"', bprice='"+bprice+"' where isbn='"+isbn+"'";
		
		st.execute(sql);
		
		System.out.println("Record Updated");
		
	}
	
	public void select() throws SQLException
	{
		String sql="select bname,isbn,bprice,bauthor from book";
		
		ResultSet rs=st.executeQuery(sql);
		ResultSetMetaData rsm=rs.getMetaData();
		
		System.out.println(rsm.getColumnName(2)+"\t"+rsm.getColumnName(1)+"\t"+rsm.getColumnName(4)+"\t"+rsm.getColumnName(3));
		
		while(rs.next())
		{
			String isbn=rs.getString(2);
			String bname=rs.getString(1);
			String bauthor=rs.getString(4);
			String bprice=rs.getString(3);
			
			System.out.println(isbn+"\t"+bname+"\t"+bauthor+"\t"+bprice);
		}
	rs.close();
	}

	public static void main(String[] args) throws SQLException, ClassNotFoundException {
		// TODO Auto-generated method stub

		try
		{
			BookMenu b1=new BookMenu();
			int choice;
			
			do
			{
				System.out.println("1:Insert");
				System.out.println("2:Delete");
				System.out.println("3:Update");
				System.out.println("4:Select");
				System.out.println("5:Exit");
				
				System.out.println("Enter ur Choice");
				 choice =sc.nextInt();
				
				switch(choice)
				{
				case 1:
					b1.insert();
					b1.select();
					break;
				
				case 2:
					b1.delete();
					b1.select();
					break;
					
				case 3:
					b1.update();
					b1.select();
					break;
					
				case 4:
					b1.select();
					break;
					
				case 5:
					System.exit(0);
					break;
					
					default:
					System.out.println("Invalid choice");
					break;
				
			}
			
			}
			while(choice != 5);
			
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

		
