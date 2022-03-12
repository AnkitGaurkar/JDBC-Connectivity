# JDBC-Connectivity

package com;
import java.sql.*;
import java.util.Scanner;
public class BookMenuJDBC {

	static Scanner sc;
	static Connection con;
	static PreparedStatement pst;
	
	public BookMenuJDBC() throws ClassNotFoundException, SQLException
	{
		Class.forName("com.mysql.cj.jdbc.Driver");
		con=DriverManager.getConnection("jdbc:mysql://localhost:3306/adjtplus","root","root");
		
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
	    
	    String sql="insert into book values(?,?,?,?)";
	    
	    pst=con.prepareStatement(sql);
	    
	    pst.setString(1, isbn);
	    pst.setString(2, bname);
	    pst.setString(3, bauthor);
	    pst.setDouble(4, bprice);
	    
	    pst.execute();
	    System.out.println("Record Inserted");
	    
	}
	public void delete() throws SQLException
	{
		System.out.println("Enter isbn");
		String isbn=sc.next();
		
		String sql="delete  from book where isbn=?";
		
		pst=con.prepareStatement(sql);
		pst.setString(1,isbn);
		
		pst.execute();
		
		System.out.println("Record Deleted");
	}
	public void update() throws SQLException
	{
		System.out.println("Entr isbn");
		String isbn=sc.next();
		System.out.println("Enter bname");
		String bname=sc.next();
		System.out.println("Enter bauthor");
		String bauthor=sc.next();
		System.out.println("Enter bprice");
		double bprice=sc.nextFloat();
		
		String sql="update book set bname=?, bauthor=?, bprice=?,where isbn=?";
		
		pst=con.prepareStatement(sql);
		pst.setString(1, bname);
		pst.setString(2, bauthor);
		pst.setDouble(3, bprice);
		pst.setString(4,isbn);
		
		pst.execute();
		
		System.out.println("Record Updated");
	}
	public void select() throws SQLException
	{
		String sql="select * from book";
		
		pst=con.prepareStatement(sql);
		
		ResultSet rs=pst.executeQuery();
		
		while(rs.next())
		{
			System.out.println(rs.getString(1)+"\t"+rs.getString(2)+"\t"+rs.getString(3)+"\t"+rs.getDouble(4));
		}
		rs.close();
		}
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		try
		{
			BookMenuJDBC b1=new BookMenuJDBC();
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
				pst.close();
				con.close();
			}
			catch(SQLException e)
			{
				e.printStackTrace();
			}
		}
	}
	

		

	}

