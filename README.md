# Virtual Class Virtual Method and Virtual Interface

VIRTUAL = MAYA
As we known Virtual means almost or nearly as described, but not completely or according to strict definition. 

# V i r t u a l    C l a s s

Virtual class is a class that cannot be directly constructed
1. A virtual class cannot be new() -ed
2. A virtual class is an abstract template that MUST be extended

By declaring a virtual class we actually create a class template. Pure virtual methods may only be declared in a virtual class (abstract class)

Common misconception: methods in virtual classes are not virtual unless declared!

# V i r t u a l    M e t h o d

Virtual method can be overridden by an extended-class method

Overriding virtual methods in extended classes requires:
1. Argument names must match
2. Argument types must match
3. Argument directions must match
4. number of arguments must match
5. Return types must match

        // Common misconception:method in virtual classes are not virtual unless declared
        module example9;
            virtual class Base1; //declare a virtual class creates a class template
                pure virtual function void showit ( arg_t i1 );
                $display ("Base1 : arg_t = %2h", i1);
                endfunction 
            endclass
          Base1 b1;  
        endmodule

# virtual Function

    Module Top;
    
      class Cmd;
      rand bit [15:0] a,b;
      rand byte opcode;
      rand bit cycle;
  
      virtual function void printmsg;
      $display ("Cmd: cmd=%h opcode=%h", {a,b}, opcode);
      endfunction
  
      endclass

      class NewCmd extends Cmd;
        virtual function void printmsg;
          $display ("NewCmd: data3=%h data2=%h opcode=%h",a,b, opcode);
        endfunction
      endclass
      
      module top;
      Cmd b1 = new();
      NewCmd e1 = new();

      task doMsg;
      b1.printmsg();
      endtask

      initial begin
        doMsg;
        b1 = e1;
        doMsg;
      end
      
    endmodule
    
V C S   S i m u l a t i o n   R e p o r t 

   Cmd: cmd=00000000 opcode=00
   
   NewCmd: data3=0000 data2=0000 opcode=00
   

# Pure Virtual Method

Pure virtual method is a method without a body that must be extended before being used
Pure virtual methods may only be declared in a virtual class (abstract class)

Virtual function only can be displayed on the top parent class, if not it will trigger error on compilation.

    module top();
  
    virtual class base;
      function void run ();
        $display("Running Base");
      endfunction
    
      pure virtual function void play();
    endclass
  
    class child extends base;
      function void run ();
        $display("Running Child");
      endfunction
    
      virtual function void play();
        $display("Playing football");
      endfunction
    endclass
    //base b;
    child c;
    initial
      begin
        //base b; 
        //b = new;
        //child c;
        c = new;
        //b.run ();
        c.run ();
        c.play();
      end
       
    endmodule

V C S   S i m u l a t i o n   R e p o r t 

Running Child

Playing football
           


   
   
   
    module top ();

    class base;
      virtual function void my_task ();
        $display ("This is base_class");
      endfunction
     endclass

    class ext_class extends base;
      function void my_task ();
        $display ("This is extended class");
      endfunction
    endclass

      base bs_hand;
      ext_class es_hand;

      initial begin
      bs_hand = new;
      es_hand = new;
      bs_hand.my_task ();
        $display ("\n Applying polymorphism : Overriding base-class method by extended class \n");
      bs_hand = es_hand; // Here polymorphism is done.
      bs_hand.my_task ();
      end
    endmodule   

V C S   S i m u l a t i o n   R e p o r t 
   
This is base_class

Applying polymorphism : Overriding base-class method by extended class 

This is extended class

Polymorphism : It’s a process to redefine a method of a derived class. In simple word the method < task / function > has to be virtual. As you can see from the above output, the task “my_task” although called using base class handle “bs_hand” the actual task getting called is the one defined in “extended class” .

    
What is happend if without virtual

      module top ();

    class base;
      function void my_task ();
        $display ("This is base_class");
      endfunction
     endclass

    class ext_class extends base;
      function void my_task ();
        $display ("This is extended class");
      endfunction
    endclass

      base bs_hand;
      ext_class es_hand;

      initial begin
      bs_hand = new;
      es_hand = new;
      bs_hand.my_task ();
        $display ("\n Applying polymorphism : Overriding base-class method by extended class \n");
      bs_hand = es_hand; // Here polymorphism is done.
      bs_hand.my_task ();
      end
    endmodule   
           
V C S   S i m u l a t i o n   R e p o r t 

This is base_class

 Applying polymorphism : Overriding base-class method by extended class 

This is base_class

As you can see from the above output, the task “my_task” although called using base class handle “bs_hand” the actual task is not getting called is the one defined in “extended class”. It still called base class.
