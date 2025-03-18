# my-first-repoimport mysql.connector as conn
import os
myconn = conn.connect(host="localhost", user="root",password="AbhijoyGogoi12@", database='school')
cursor = myconn.cursor()

#*********************************************************************

def Display_Stu_Class():
        ans='y'
        while ans=='y'or ans=='Y':
                print('\nPlease Enter which class you want to view')
                cls=int(input('class :  '))
                cursor.execute("select Name,Gender,DOB,City from student,enroll where student.Admno=enroll.Adm_no and enroll.Class_id={}".format(cls))

                data=cursor.fetchall()
                print('+--------------------+--------------------+--------------------+--------------------+')
                print('|     Name           |     Gender         |      DOB           |      City          |')
                print('+--------------------+--------------------+--------------------+--------------------+')
               
                for i in range(len(data)):
                    print('|   ',end='')    
                    for j in range(len(data[i])):
                        str1=str(data[i][j])
                        n=len(str1)
                        m=17-n
                        print(str1+' '*m, end='|   ')
                    print('   ')
                    
                    print('+--------------------+--------------------+--------------------+--------------------+')
                    
                ans=input('Display another Record (y/n): ')
                    
#*********************************************************************
                
def Display_All():
        ans='y'
        while ans=='y'or ans=='Y':
                cursor.execute("select * from student")

                data=cursor.fetchall()
                print('+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+')
                print('|      Admn No.      |        Name        |    Father\'s Name   |     Mother\'s name  |        Gender      |         DOB        |         Phno       |          City      |')
                print('+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+')
               
                for i in range(len(data)):
                    print('|   ',end='')    
                    for j in range(len(data[i])):
                        str1=str(data[i][j])
                        n=len(str1)
                        m=17-n
                        print(str1+' '*m, end='|   ')
                    print('   ')
                    
                    print('+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+')
                    
                ans='n'
                    

#*********************************************************************

def Display_Class():
        ans='y'
        while ans=='y'or ans=='Y':
                cursor.execute("select * from class")

                data=cursor.fetchall()
                print('+--------------------+--------------------+--------------------+')
                print('|          Id        |     Class Name     |       Capacity     |')
                print('+--------------------+--------------------+--------------------+')
               
                for i in range(len(data)):
                    print('|   ',end='')    
                    for j in range(len(data[i])):
                        str1=str(data[i][j])
                        n=len(str1)
                        m=17-n
                        print(str1+' '*m, end='|   ')
                    print('   ')
                    
                    print('+--------------------+--------------------+--------------------+')
                    
                ans='n'

#*********************************************************************

def Add_Student():
    ans='y'
    while ans=='y'or ans=='Y':
        cursor.execute("select * from student")
        d=cursor.fetchall()        
        c1 =cursor.rowcount+230000+1    
        c2 = input("Please enter the name: ")
        c3 = input("Please enter father's name: ")
        c4 = input("Please enter mother's name: ")
        c5 = input("Please enter the gender: ")
        c6 = input("Please enter the date of birth (YYYY-MM-DD): ")
        c7 = int(input("Please enter the phone number: "))
        c8 = input("Please enter the city: ")         
 
        cursor.execute("INSERT INTO student  VALUES({},'{}','{}','{}','{}','{}',{},'{}')".format(c1,c2,c3,c4,c5,c6,c7,c8))  
        myconn.commit()  
        print("Data inserted successfully!")
        ans=input('Add more records (y/n): ')

#*********************************************************************
         
def Add_Class():
        ans='y'
        while ans=='y'or ans=='Y':
                cursor.execute("select * from class")
                d=cursor.fetchall()        
                n1 =cursor.rowcount+1
                n2 = int(input("Enter Class name: "))
                n3 = int(input("Enter  capacity: "))
                cursor.execute("INSERT INTO class  VALUES({},{},{})".format(n1,n2,n3))  
                myconn.commit()  
                print("Data inserted successfully!")
                ans=input('Add more records (y/n): ')
                
#*********************************************************************
                
def Add_Enroll():
    ans='y'
    while ans=='y'or ans=='Y':
        b1 = int(input("Enter Admission no: "))
        b2 = int(input("Enter rollno: "))
        b3 = int(input("Enter class id: "))
        cursor.execute("INSERT INTO enroll  VALUES({},{},{})".format(b1,b2,b3))  
        myconn.commit()  
        print("Data inserted successfully!")
        ans=input('Add more records (y/n):')
        
#*********************************************************************
                 
def Add_Admin():
    ans='y'
    while ans=='y'or ans=='Y':
        cursor.execute("select * from admin")
        d=cursor.fetchall()        
        c1 =cursor.rowcount+1
        c2 = input("Enter Username: ")
        c3 = input("Enter password: ")
        cursor.execute("INSERT INTO admin  VALUES({},'{}','{}')".format(c1,c2,c3))  
        myconn.commit()  
        print("Data inserted successfully!")
        ans=input('Add more records (y/n):')
#*********************************************************************
def Update_Stu():
     while True:
                print('\n\n+--------------------------------+')    
                print("|      Update Student  Menu      |")                 
                print('+--------------------------------+')      
                print("|      1 - Update Name           |")        
                print('+--------------------------------+')
                print("|      2 - Update Father\'s name  |")
                print('+--------------------------------+')        
                print("|      3 - Update Mother\'s name  |")
                print('+--------------------------------+')
                print("|      4 - Update Gender         |")
                print('+--------------------------------+')
                print("|      5 - Update DOB            |")
                print('+--------------------------------+')
                print("|      6 - Update Phone number   |")
                print('+--------------------------------+')
                print("|      7 - Update City           |")
                print('+--------------------------------+')
                print("|      8 - Close                 |")
                print('+--------------------------------+') 
                n = input("\nSelect what you want to update:  ")
                
                            
                if n=='1':
                        ad=int(input('enter the admission number: '))
                        
                        new_name=input('Enter new name : ')
                        cursor.execute("update student set Name='{}' where Admno={}".format(new_name,ad))
                        myconn.commit()
                elif n=='2':
                     name=input('Enter  name : ')
                     new_F_name=input('Enter new Father\'s name : ')
                     
                     cursor.execute("update student set F_Name='{}' where Name='{}'".format(new_F_name,name))
                     myconn.commit()
                elif n=='3':
                     name=input('Enter  name : ')
                     new_M_name=input('Enter new Mother\'s name : ')
                     
                     cursor.execute("update student set M_Name='{}' where Name='{}'".format(new_M_name,name))
                     myconn.commit() 
                elif n=='4':
                     name=input('Enter  name : ')
                     newgender=input('Enter new gender : ')
                     
                     cursor.execute("update student set Gender='{}' where Name='{}'".format(newgender,name))
                     myconn.commit()
                elif n=='5':
                     name=input('Enter  name : ')
                     newdob=input('Enter new DOB(yyyy-mm-dd) : ')
                     
                     cursor.execute("update student set DOB='{}' where Name='{}'".format(newdob,name))
                     myconn.commit()
                elif n=='6':
                     name=input('Enter  name : ')
                     newpno=input('Enter new phone number : ')
                     
                     cursor.execute("update student set Phno='{}' where Name='{}'".format(newpno,name))
                     myconn.commit()
                elif n=='7':
                     name=input('Enter  name : ')
                     newcity=input('Enter new city name : ')
                     
                     cursor.execute("update student set City='{}' where Name='{}'".format(newcity,name))
                     myconn.commit()
                elif n=='8':
                       break               
                else:
                        print("\ninvalid Input!")
#*********************************************************************
def Update_Class():
     while True:
                print('\n\n+--------------------------------+')    
                print("|      Update Class menu         |")                 
                print('+--------------------------------+')      
                print("|      1 - Update Class Name     |")        
                print('+--------------------------------+')
                print("|      2 - Update Capacity       |")
                print('+--------------------------------+')        
                print("|      3 - Close                 |")
                print('+--------------------------------+')        
                n = input("\nSelect what you want to update:  ")
                            
                if n=='1':
                     id1=int(input('Enter the Id :  '))
                     new_user=input('Enter new class name : ')
                     cursor.execute("update class set Name={} where Id={}".format(new_user,id1))
                     myconn.commit()
                elif n=='2':
                     
                     c_name=input('Enter class name: ')
                     cap=input('Enter new capacity: ')
                     cursor.execute("update class set capacity={} where username='{}'".format(cap,c_name))
                     myconn.commit()
                elif n=='3':
                        break
                
                else:
                        print("\ninvalid Input!")
#*********************************************************************
def Delete_Stu():
        ad=int(input('enter the admission number: '))
        cursor.execute("select * from enroll where Adm_no={}".format(ad))
        data=cursor.fetchall()
        if cursor.rowcount==0:
                cursor.execute("delete from student  where Admno={}".format(ad))
                print('record successfully deleted')
                myconn.commit()
        
        else:
                print('you cannot delete parent data')
#*********************************************************************
def Delete_Class():
        id=int(input('enter the class id: '))
        
        cursor.execute("select * from enroll where Class_id={}".format(id))
        data=cursor.fetchall()
        if cursor.rowcount==0:               
        
                cursor.execute("delete from class  where Class_id={}".format(id))
                print('record successfully deleted')
                myconn.commit()
        else:
                print('you cannot delete parent data')        

#*********************************************************************
def Delete_Admin():
        ad=int(input('enter the admin id: '))
                        
        
        cursor.execute("delete from Admin  where id={}".format(ad))
        print('record successfully deleted')
        myconn.commit()
#*********************************************************************
#*********************************************************************
def Update_Admin():
         while True:
                print('\n\n+---------------------------------+')    
                print("|      Update Admin Menu         |")                 
                print('+--------------------------------+')      
                print("|      1 - Update Username       |")        
                print('+--------------------------------+')
                print("|      2 - Update Password       |")
                print('+--------------------------------+')        
                print("|      3 - Close                 |")
                print('+--------------------------------+')        
                n = input("\nSelect what you want to update:  ")
                            
                if n=='1':
                     id1=int(input('Enter the Id :  '))
                     new_user=input('Enter new username : ')
                     cursor.execute("update Admin set username='{}' where id={}".format(new_user,id1))
                     myconn.commit()
                elif n=='2':
                     
                     new_user=input('Enter username : ')
                     new_pass=input('Enter new Password : ')
                     cursor.execute("update Admin set password='{}' where username='{}'".format(new_user,new_pass))
                     myconn.commit()
                elif n=='3':
                        break
                
                else:
                        print("\ninvalid Input!")
#*********************************************************************                        
def Insert_Data():
         while True:
                print('\n\n+--------------------------+')    
                print("|            menu          |")                 
                print('+--------------------------+')      
                print("|      1 - Add Student     |")        
                print('+--------------------------+')  
                print("|      2 - Add Class       |")
                print('+--------------------------+')        
                print("|      3 - Enroll Student  |")
                print('+--------------------------+') 
                print("|      4 - Add Admin       |")
                print('+--------------------------+')        
                print("|      5 - Close           |")
                print('+--------------------------+')        
                n = input("\nplease enter your choice:  ")
                            
                if n=='1':
                        Add_Student()
                elif n=='2':
                        Add_Class()
                elif n=='3':
                        Add_Enroll()
                elif n=='4':
                        Add_Admin() 
                elif n=='5':
                        break
                else:
                        print("\ninvalid Input!")
                        
#*********************************************************************
                        
def Display():
        while True:
                print('\n\n+----------------------------------------+')    
                print("|       Display menu                      |")                 
                print('+-----------------------------------------+')      
                print("|      1 - Display Students per Class     |")        
                print('+-----------------------------------------+')
                print("|      2 - Display All Students           |")
                print('+-----------------------------------------+')       
                print("|      3 - Display Class Data             |")
                print('+-----------------------------------------+')        
                print("|      4 - Close                          |")
                print('+-----------------------------------------+')        
                n = input("\nplease enter your choice:  ")
                            
                if n=='1':
                        Display_Stu_Class()
                elif n=='2':
                        Display_All()
                elif n=='3':
                        Display_Class()
                elif n=='4':
                        break
                else:
                        print("\ninvalid Input!")
                        
#*********************************************************************
                                
def update():
       while True:
                print('\n\n+----------------------------------------+')    
                print("|       Update  menu                      |")                 
                print('+-----------------------------------------+')      
                print("|      1 - Update Students data           |")        
                print('+-----------------------------------------+')
                print("|      2 - Update Class data              |")   
                print('+-----------------------------------------+')
                print("|      3 - Update Admin                   |")
                print('+-----------------------------------------+')
                print("|      4 - Close                          |")
                print('+-----------------------------------------+')        
                n = input("\nplease enter your choice:  ")
                            
                if n=='1':
                        Update_Stu()
                elif n=='2':
                        Update_Class()
                
                elif n=='3':
                        Update_Admin()
                elif n=='4':
                        break
                else:
                        print("\ninvalid Input!")

#*********************************************************************

def delete():
   while True:
                print('\n\n+----------------------------------------+')    
                print("|       Delete  menu                      |")                 
                print('+-----------------------------------------+')      
                print("|      1 - Delete Students                |")        
                print('+-----------------------------------------+')
                print("|      2 - Delete Class data              |")   
                print('+-----------------------------------------+')
                print("|      3 - Delete Admin                   |")
                print('+-----------------------------------------+')
                print("|      4 - Close                          |")
                print('+-----------------------------------------+')        
                n = input("\nplease enter your choice:  ")
                            
                if n=='1':
                        Delete_Stu()
                elif n=='2':
                        Delete_Class()
                
                elif n=='3':
                        Delete_Admin()
                elif n=='4':
                        break
                else:
                        print("\ninvalid Input!")
     
#*********************************************************************


while True:
    os.system('clear')
    print('\n\n+-------------------------------------------+')
    print("|          STUDENT MANAGEMENT SYSTEM        |")
    print('+-------------------------------------------+')
    print('|           Press 1 to view students        |')
    print('+-------------------------------------------+')
    print('|           Press 2 to for Admin log in     |')
    print('+-------------------------------------------+')
    print('|           Press 3 to Exit                 |')
    print('+-------------------------------------------+')
    
    n = input("\n\nplease enter your choice : ")
    if n=='1':
        Display_Stu_Class()
    elif n=='2':

        print('Adminlogin')
        username=input('enter username: ')
        passd=input('enter password')
        cursor.execute("select * from admin where username='{}'".format(username))
        data=cursor.fetchall()
        if cursor.rowcount>0:
                if data[0][2]==passd:
                        while True:
                            print('\n\n+-----------------------+')    
                            print("|         menu          |")                 
                            print('+-----------------------+')      
                            print("|      1 - Display      |")        
                            print('+-----------------------+')  
                            print("|      2 - Insert       |")
                            print('+-----------------------+')        
                            print("|      3 - Delete       |")
                            print('+-----------------------+') 
                            print("|      4 - Update       |")
                            print('+-----------------------+')        
                            print("|      5 - Close        |")
                            print('+-----------------------+')        
                            n = input("\nplease enter your choice: ")
                            
                            if n=='1':
                                Display()
                            elif n=='2':
                                Insert_Data()
                            elif n=='3':
                                delete()
                            elif n=='4':
                                update() 
                            elif n=='5':
                                 break
                            else:
                                print("\ninvalid Input!")
                
                        #-----------------------
                else:
                        print('\n***invalid Password!*** \n')
        else:
                print('\n***invalid Username!***\n')
            
    elif n=='3':
        break    
    else:
        print("invalid Input!")
        
#*********************************************************************


myconn.close()
exit()
     

