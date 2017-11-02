# assignment-one

////////////User //////////////

package MovieRecommender;

import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.util.Scanner;
import java.io.IOException;
 

public class User {
    String name;
    String age;
    String sex;
    String occupation;
    
    public User(String name,String age,String sex,String occupation){
        this.name= name;
        this.age= age;
        this.sex = sex;
        this.occupation = occupation;    
    }
    
    
    public String getName(){
        return name;
    }
    
    public String getSex(){
        return sex;
    }
    
    
    public String getAge(){
        return age;
    }
    
    public String getOccupation(){
        return occupation;
    }
    
    public void setName(String Nname){
        this.name = Nname;
    }
    
    public void setSex(String NSex){
        this.name = NSex;
    }
    
    public void setAge(String NAge){
        this.name = NAge;
    }
    
    public void setOccupation(String NOccupation){
        this.name = NOccupation;
    }
}



/////////////////////ManageUser//////////////////

package MovieRecommender;


import java.util.*;


public class ManageUser {
    
    static List<User> UserList = new LinkedList<User>();
    public static void main(String[] agrs){
        
        
        select(UserList);        
                
    }

    
    
    private static void select(List<User> UserList ){
        System.out.println("***************");
        System.out.println("*Welcom *");
        System.out.println("*1：Add User                    *");
        System.out.println("*2：Delete User                 *");
        System.out.println("*3：Modify User                 *");
        System.out.println("*4：List User                   *");
        System.out.println("***************");
        
        System.out.println("Enter Operation Option: ");
        Scanner sc = new Scanner(System.in);
        int choice = sc.nextInt();        
        switch(choice){
        //add 
        case 1:
            System.out.print("Enter User Name：");
            Scanner Uname = new Scanner(System.in);
            String name = Uname.nextLine();
            System.out.print("Enter User Age：");
            Scanner Uage = new Scanner(System.in);
            String age = Uage.nextLine();
            System.out.print("Enter User Gender：");
            Scanner Usex = new Scanner(System.in);
            String sex = Usex.nextLine();
            System.out.print("Enter User Occupation：");
            Scanner Uocc = new Scanner(System.in);
            String occupation = Usex.nextLine();
            UserList.add(new User(name,age,sex,occupation));
            System.out.println("Added success！！！！！");
            select(UserList);
            break;
            
        //delete
        case 2:
            System.out.print("Enter User Name(Delete)：");
            Scanner Uname1 = new Scanner(System.in);
            String UuserId = Uname1.nextLine();
            boolean isfindDelete = false;
            for (int i = 0; i < UserList.size(); i++) {
                if(UuserId.equals(UserList.get(i).getName())){
                    System.out.println("Deleting");
                    UserList.remove(i);
                    System.out.println("success deleted!!!");
                    isfindDelete =true;
                }
            }
            if(!isfindDelete){
                System.out.println("Invalid input");
            }
            select(UserList);
           break;
        //modify
        case 3:
            System.out.print("Enter User Name(modify)：");
            Scanner Nname = new Scanner(System.in);
            String NUserName = Nname.nextLine();
            boolean isfindChange = false;
            for (int j = 0; j < UserList.size(); j++) {
                if(NUserName.equals(UserList.get(j).getName())){
                    System.out.println("changing");
                    System.out.println("User Name was"+UserList.get(j).getName());
                    System.out.print("Enter New Name：");
                    Scanner name1 = new Scanner(System.in);
                    String name2 = name1.toString();
                    UserList.get(j).setName(name2);
                    System.out.println("Changed success!!!");
                    isfindChange =true;
                }else{
                    
                }
            }
            if(!isfindChange){
                System.out.println("Invalid input");
            }
            select(UserList);
            break;
        //list
        case 4:
            System.out.print("All User Details：");
            for (int i = 0; i < UserList.size(); i++) {
            		System.out.println("   ");
                    System.out.println("Name:"+UserList.get(i).getName());
                    System.out.println("Age:"+UserList.get(i).getAge());
                    System.out.println("Sex:"+UserList.get(i).getSex());
                    System.out.println("Occupation:"+UserList.get(i).getOccupation()); 
                
            }
            break;
        }
        
    }
}


///////////////////////MovieRating////////////////

package MovieRecommender; 
  
import javax.swing.*; 
  
import java.awt.*; 
import java.awt.event.*; 
  
public class MovieRating { 
  public static void main(String[] args) { 
    MovieSys filmSys=new MovieSys("movie rating"); 
    filmSys.initWin(); 
  }  
} 
class MovieSys extends JFrame{ 
    
  private JPanel p1,p2,p3,combop; 
  private JTabbedPane tab; 
  private Container container; 
  private JButton b1,b2; 
  private Listener listener; 
  private Label nameLabel; 
  private Label occupationLabel; 
  private Label showLabel; 
  private JTextField textName; 
  private JTextField textoccupation; 
  private TextArea showoccupationArea; 
  
   // search 
  
  private Label searchLabel; 
  private JTextField searchText; 
  private JButton sBut; 
  private JTextField resultText; 
  private String[] name; 
  private String[] occupation; 
    
   
  //sort order 
  
  private TextArea showTextArea; 
  private JButton sortBut; 
  private int countNum=0; 
  private JButton clearBut; 
  public MovieSys(String str){ 
    super(str); 
      
    this.name=new String[100]; 
    this.occupation=new String[100]; 
    listener = new Listener(); 
    tab = new JTabbedPane(JTabbedPane.TOP);  
     
    container = this.getLayeredPane(); 
  
    combop = new JPanel(); 
    p1 = new JPanel(); 
    p2 = new JPanel(); 
    p3 = new JPanel(); 
      
    b1 =new JButton("confirm"); 
    b2 =new JButton("withdraw"); 
    nameLabel =new Label("Movie Name"); 
    occupationLabel =new Label("Rating"); 
      
    showLabel=new Label("None Store"); 
      
    textName =new JTextField(15); 
    textoccupation =new JTextField(15); 
    showoccupationArea=new TextArea(); 
      
    //search2 
 
    searchLabel=new Label("Enter Movie Name："); 
    searchText=new JTextField(15); 
    sBut=new JButton("search"); 
    resultText=new JTextField(15); 
    
    //sort order2 
    
    showTextArea=new TextArea(); 
    sortBut=new JButton("Rating Order"); 
    clearBut=new JButton("Delete All"); 
  } 
  public void initWin(){ 
    this.setBounds(300, 300, 500, 400); 
    this.addWindowListener(new WindowAdapter(){ 
      public void windowClosing(WindowEvent e) { 
        super.windowClosing(e); 
        System.exit(0); 
      }}); 
      layoutWin(); 
      this.setVisible(true); 
  } 
  private void layoutWin(){ 
      
    tab.add(p1,"Enter Rating"); 
    tab.add(p2,"Search Rating"); 
    tab.add(p3,"Rating Order"); 
    combop.add(new JLabel("Movie")); 
    container.setLayout(new BorderLayout()); 
    container.add(combop,BorderLayout.NORTH); 
    container.add(tab,BorderLayout.CENTER); 
      
    Container con1=new Container(); 
    con1.setLayout(new FlowLayout()); 
    con1.add(nameLabel); 
    con1.add(textName); 
      
    con1.add(occupationLabel); 
    con1.add(textoccupation); 
    p1.add(con1,BorderLayout.NORTH); 
    p1.add(con1); 
    p1.add(showoccupationArea); 
      
    Container con2=new Container(); 
    con2.setLayout(new FlowLayout()); 
    con2.add(b1); 
    con2.add(b2); 
    con2.add(showLabel); 
    p1.add(con2); 
    b1.addActionListener(listener); 
    b2.addActionListener(listener); 
    
      
    Container con3=new Container(); 
    con3.setLayout(new FlowLayout()); 
    con3.add(searchLabel); 
    con3.add(searchText); 
    con3.add(sBut); 
    p2.add(con3,BorderLayout.NORTH); 
    sBut.addActionListener(listener); 
    p2.add(resultText); 
    
    p3.add(showTextArea); 
    p3.add(sortBut); 
    p3.add(clearBut); 
    sortBut.addActionListener(listener); 
    clearBut.addActionListener(listener); 
  } 
  
  
  class Listener implements ActionListener{ 
   
      public void actionPerformed(ActionEvent e) { 
        
      if(e.getSource()==b1){ 
          
        if((textName.getText().equals(""))||(textoccupation.getText().equals(""))){ 
          showLabel.setText("Fail(Invaild enter)！"); 
        } 
        else{ 
          name[countNum]=textName.getText(); 
          occupation[countNum]=textoccupation.getText(); 
          countNum++; 
          String area="Enter Success"+countNum+"Store"; 
          showLabel.setText(area); 
          sortMess(false); 
          textName.setText(""); 
          textoccupation.setText(""); 
        } 
          
      } 
      if(e.getSource()==b2){ 
        if(countNum>0){ 
          countNum--; 
          String area="Delate Success"+countNum+"Store"; 
          showLabel.setText(area); 
          sortMess(false); 
        } 
      } 
      if(e.getSource()==sBut){ 
        if(!searchText.getText().equals("")){ 
          searchMess(searchText.getText()); 
        } 
      } 
      if(e.getSource()==sortBut){ 
        sortMess(true); 
      } 
      if(e.getSource()==clearBut){ 
        if(!showTextArea.getText().equals("")){ 
          showTextArea.setText(""); 
         } 
      } 
    } 
      
    public void sortMess(boolean sign) { 
      // TODO Auto-generated method stub 
      if(sign){ 
        for(int i=0;i<countNum;i++){ 
          for(int j=i+1;j<countNum;j++){ 
            if(Integer.parseInt(occupation[i])<Integer.parseInt(occupation[j])){ 
              String s1,s2; 
              s1=name[i]; 
              s2=occupation[i]; 
                
              name[i]=name[j]; 
              occupation[i]=occupation[j]; 
                
              name[j]=s1; 
              occupation[j]=s2; 
            } 
          } 
        } 
      }else{  
        
        if(!showoccupationArea.getText().equals("")){ 
          showoccupationArea.setText(""); 
        } 
      } 
      for(int i=0;i<countNum;i++){ 
        String content="Movie Name:"+name[i]+"\t"+"Rating:"+occupation[i]; 
        if(sign)showTextArea.append(content+"\n"); 
        else showoccupationArea.append(content+"\n"); 
      } 
    } 
      
    public void searchMess(String n) { 
      // TODO Auto-generated method stub 
        
      for(int i=0;i<countNum;i++){ 
        if(name[i].equals(n)){ 
          String content="Movie Name: "+name[i]+"   "+"Rating:"+occupation[i]; 
          resultText.setText(content); 
          return; 
        } 
      } 
      resultText.setText("Invalid Movie"); 
    } 
  } 
}


