# Virtual-Class-Virtual-Method-and-Virtual-Interface


# Pure Virtual Function 

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
