# PhysicalEducation

/**
 * PhysicalEducation Class
 * This class allows user to input a number
 * of students and displays their height,
 * weight and BMI results.
 */
package physicaleducation;
import java.util.*;
public class PhysicalEducation {

	public static void main (String[] args){
		PhysicalEducation program;
		try{
			program = new PhysicalEducation();
			program.run();
		} catch(Exception x){
			x.printStackTrace();
		}
		System.exit(0);
	}

	/**
	 * run Method
	 * This method reads the number of students
	 * provided by the user of the program. Executes
	 * populateStudent, sortStudent, and showStudent
	 * methods.
	 */
    public void run() {
    	int n = readNo("Number of Students");
    	Student[] stud= new Student[n];
 		populateStudent(stud);
 		sortStudent(stud);
 		showStudent(stud);
    }

    /**
     * showStudent Method
     * This method prints a list of students with
     * their name, height, weight and BMI info.
     * @param stud This is the only parameter to the showStudent method
     */
  	public void showStudent(Student[] stud){
  		System.out.println("");
  		System.out.println("List of Students");
  		System.out.printf("%15s%10s%10s%20s%n","Name","Height","Weight","BMI");
		for (int count=0; count<stud.length; count++){
			System.out.printf("%15s%10d%10d%20s%n", stud[count].getName(),stud[count].getHeight(),stud[count].getWeight(),getBMI(stud[count].getHeight(),stud[count].getWeight()));
		}
 	}

 	/**
 	 * getBMI Method
 	 * This method returns the BMI result.
 	 * Results may be "Severly underweight", "Underweight",
 	 * "Normal", "Overweight", or "Obeses".
 	 * @param height This is the first parameter to the getBMI method
 	 * @param weight This is the second parameter to the getBMI method
 	 * @return String This returns the BMI result.
 	 */
  	public String getBMI(int height, int weight){
  		double result = ((double)weight/((double)height*(double)height))*10000;
  		String BMI = "";
  		if (result<16){
  			BMI = "Severely underweight";
  		}
  		else if(result>=16 && result <18.5){
 			BMI = "Underweight";
  		}
 		else if(result>=18.5 && result <25){
 			BMI = "Normal";
 		}
 		else if(result>=25 && result <30){
 			BMI = "Overweight";
 		}
 		else {
 			BMI = "Obese";
 		}
 		return BMI;
	}

	/**
	 * sortStudent Method
	 * This method sorts the given students by
	 * their name.
	 * @param stud This is the only parameter to the sortStudent method
	 */
 	public void sortStudent(Student[] stud){
 		int targetIndex=0;
 		for (int index=0; index< stud.length-1; index++){
			targetIndex= index;
 			for (int checkIndex=index+1; checkIndex < stud.length; checkIndex++){
 				if (stud[targetIndex].getName().compareTo(stud[checkIndex].getName())>0)
 					targetIndex = checkIndex;
 			}

 			if (targetIndex != index ){
 				Student temp = stud[index];
 				stud[index] = stud[targetIndex];
 				stud[targetIndex] = temp;
 			}
 		}
 	}

 	/**
 	 * populateStudent Method
 	 * This method allows user to enter the
 	 * data for the students.
 	 * @param stud This is the only parameter to the populateStudent method
 	 */
  	public void populateStudent(Student[] stud){
		for (int count=0; count<stud.length; count++){
			System.out.println("");
			System.out.println("Enter data for Student "+ (count+1) );
			stud[count] = readStudentInfo();
		}
		return;
 	}

 	/**
 	 * readStudentInfo Method
 	 * This methods reads the name, heigh, and weight
 	 * input of each student provided by the user of
 	 * the program.
 	 * @return Student This returns the data of each students
 	 */
  	public Student readStudentInfo(){
		String name = readString("Enter name of student");
		int height = readHeight("Enter height of student");
		int weight = readWeight("Enter weight of student");
		Student student = new Student(name,height,weight);
		return student;
 	}

 	/**
 	 * readNo Method
 	 * This method reads the number provided by the
 	 * user of the program. A warning is given when
 	 * and integer isn't provided or if the age of the
 	 * student is younger than 1 or older than 50.
 	 * @param prompt This is the only parameter to the readNo method
 	 * @return int This returns the number provided by the user
 	 * of the program
 	 */
	public int readNo(String prompt){
       Scanner scan = new Scanner(System.in);
       int r = 0;
       boolean noProblem = true;
       do {
         try {
         	System.out.print(prompt + ": ");
			r=Integer.parseInt(scan.nextLine());
			noProblem = true;
         }catch (Exception x){
       	    System.out.println("You must enter an integer.");
       	    noProblem = false;
         }
         if ( r < 1  || r > 50 )
             System.out.println("The student's age must be a number from 1 to 50.");
       } while (noProblem == false || r < 1 || r > 50);
       return r;
    }

    /**
     * readHeight Method
     * This method reads the given height of the student.
     * Displays a warning if an integer isn't provided or when
     * the height of the student is lower than 130 or higher
     * than 215.
     * @param prompt This is the only parameter to the readHeight method
     * @return int This returns the height info of the student
     */
	public int readHeight(String prompt){
       Scanner scan = new Scanner(System.in);
       int r = 0;
       boolean noProblem = true;
       do {
         try {
         	System.out.print(prompt + ": ");
			r=Integer.parseInt(scan.nextLine());
			noProblem = true;
         }catch (Exception x){
       	    System.out.println("You must enter an integer.");
       	    noProblem = false;
         }
         if ( r < 130  || r > 215 )
             System.out.println("The student's height must be a number from 130 to 215.");
       } while (noProblem == false || r < 130 || r > 215);
       return r;
    }

    /**
     * readWeight Method
     * This method reads the weight of the student.
     * Displays a warning if an integer isn't provided
     * or when the weight is lower than 25 or higher than 115.
     * @param prompt This is the only parameter to the readWeight method
     * @return int This returns the weight info of the student
     */
	public int readWeight(String prompt){
       Scanner scan = new Scanner(System.in);
       int r = 0;
       boolean noProblem = true;
       do {
         try {
         	System.out.print(prompt + ": ");
			r=Integer.parseInt(scan.nextLine());
			noProblem = true;
         }catch (Exception x){
       	    System.out.println("You must enter an integer.");
       	    noProblem = false;
         }
         if ( r < 25  || r > 115 )
             System.out.println("The student's weight must be a number from 25 to 115.");
       } while (noProblem == false || r < 25 || r > 115);
       return r;
    }

    /**
     * readString Method
     * This method reads the String input provided
     * by the user of the program.
     * @param prompt This is the onyl parameter to the readString method
     * @return String This returns the String input provided by
     * the user of the program
     */
	public String readString(String prompt){
		Scanner scan = new Scanner(System.in);
		System.out.print(prompt + ": ");
		String result = scan.nextLine();
		return result;
	}
} //end of PhysicalEducation class

class Student {
		public String name;
		public int height;
		public int weight;

    public Student() {
		name = "";
		height = 0;
		weight = 0;
    }

	public Student(String name, int height, int weight){
	    this.name = name;
	    this.height = height;
	    this.weight = weight;
	}

	public String getName(){
	     return name;
	}

	public int getHeight(){
	     return height;
	}

	public int getWeight(){
	     return weight;
	}

	public void setName(String name){
	    this.name = name;
	}

	public void setHeight(int height){
	     this.height = height;
	}

	public void getWeight(int weight){
	     this.weight = weight;
	}

	public String toString(){
	    return (name+","+height+","+weight);
	}
}
