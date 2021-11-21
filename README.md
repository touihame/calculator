# calculator
rapport N3 (RANIA TOUIHAME / MOHAMED AMINE KEBDANI)


# signal and slots
# setup
first we'll find a Qt project to that create the main widget as a custom class in the starter project <Callcultaor.zip>.

   *We have to configure and Run the project. we should see a main widget with the calculator buttons.

   *let's investigate the header file calculator.h to get a clear idea about the *attributes** of the class.

   *we should special attention to the following attributes:

      1. QVector<QPushButton*> digits which store a pointer to each digit.
      2. QVector<QPUshButton*> opertions same but for the operations buttons.
      3. QPushButton *enter the enter button.
      
      
In order to have a computing functionality, we will represent any mathematical operation by:

      left   (op)  right
      
Hence we will add the following private members to our class calculator.h.

     private:
         int * left;          //left operand
         int * right;         // right operand
         QString *operation;  // Pointer on the current operation  
         
 # Custom Slots 
 
Our first step is to respond to each digit click. But here we face a classical problem which to map multiple signals to the same slot. The slot has to behave differently according the which digit was pressed. This problem is thoroughly investigated in J.Blanchette Blog.

The trivial solution is to create a slot for each button, but that will be cumbersome.

    public slots:
        void button0Clicked();
        void button1Clicked();
        ...
        void button9Clicked(); 
        

For our case, we will use the Sender approach which allow a slot to get the identity of the sender object. From that we could get which button was clicked. Hence we will define only one slot such as:

    public slots:
        void newDigit();        
      
      
      
      
   # fichier header calculator.h

<pre style="color:#000000;background:#ffffff;"><span style="color:#004a43; ">#</span><span style="color:#004a43; ">ifndef</span><span style="color:#004a43; "> CALCULATOR_H</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">define</span><span style="color:#004a43; "> CALCULATOR_H</span>

<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QMainWindow</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QGridLayout</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QVector</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QPushButton</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QHBoxLayout</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QLCDNumber</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QString</span><span style="color:#800000; ">&gt;</span>

<span style="color:#800000; font-weight:bold; ">class</span> Calculator <span style="color:#800080; ">:</span> <span style="color:#800000; font-weight:bold; ">public</span> <span style="color:#603000; ">QWidget</span>
<span style="color:#800080; ">{</span>
    <span style="color:#004a43; ">Q_OBJECT</span>
<span style="color:#800000; font-weight:bold; ">public</span><span style="color:#e34adc; ">:</span>
    Calculator<span style="color:#808030; ">(</span><span style="color:#603000; ">QWidget</span> <span style="color:#808030; ">*</span>parent <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">nullptr</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#808030; ">~</span>Calculator<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

<span style="color:#696969; ">// Add you custom slots here</span>
<span style="color:#800000; font-weight:bold; ">public slots</span><span style="color:#e34adc; ">:</span>
   <span style="color:#800000; font-weight:bold; ">void</span> newDigit<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
   <span style="color:#800000; font-weight:bold; ">void</span> changeOperation<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>  <span style="color:#696969; ">//Slot to handle the click on operations</span>
<span style="color:#800000; font-weight:bold; ">protected</span><span style="color:#e34adc; ">:</span>
    <span style="color:#800000; font-weight:bold; ">void</span> createWidgets<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>        <span style="color:#696969; ">//Function to create the widgets</span>
    <span style="color:#800000; font-weight:bold; ">void</span> placeWidget<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>         <span style="color:#696969; ">// Function to place the widgets</span>
    <span style="color:#800000; font-weight:bold; ">void</span> makeConnexions<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>      <span style="color:#696969; ">// Create all the connectivity</span>

<span style="color:#696969; ">//events</span>
<span style="color:#800000; font-weight:bold; ">protected</span><span style="color:#e34adc; ">:</span>
    <span style="color:#800000; font-weight:bold; ">void</span> keyPressEvent<span style="color:#808030; ">(</span><span style="color:#603000; ">QKeyEvent</span> <span style="color:#808030; ">*</span>e<span style="color:#808030; ">)</span>override<span style="color:#800080; ">;</span>     <span style="color:#696969; ">//Override the keypress events</span>

<span style="color:#800000; font-weight:bold; ">private</span><span style="color:#e34adc; ">:</span>
    <span style="color:#603000; ">QHBoxLayout</span> <span style="color:#808030; ">*</span>CcossinLayout<span style="color:#800080; ">;</span>
    <span style="color:#603000; ">QGridLayout</span> <span style="color:#808030; ">*</span>buttonsLayout<span style="color:#800080; ">;</span> <span style="color:#696969; ">// layout for the buttons</span>
    <span style="color:#603000; ">QVBoxLayout</span> <span style="color:#808030; ">*</span>layout<span style="color:#800080; ">;</span>        <span style="color:#696969; ">//main layout for the button</span>
    <span style="color:#603000; ">QVector</span><span style="color:#800080; ">&lt;</span><span style="color:#603000; ">QPushButton</span><span style="color:#808030; ">*</span><span style="color:#800080; ">&gt;</span> digits<span style="color:#800080; ">;</span>  <span style="color:#696969; ">//Vector for the digits</span>
    <span style="color:#603000; ">QPushButton</span> <span style="color:#808030; ">*</span>enter<span style="color:#800080; ">;</span>            <span style="color:#696969; ">// enter button</span>
    <span style="color:#603000; ">QVector</span><span style="color:#800080; ">&lt;</span><span style="color:#603000; ">QPushButton</span><span style="color:#808030; ">*</span><span style="color:#800080; ">&gt;</span> operations<span style="color:#800080; ">;</span> <span style="color:#696969; ">//operation buttons</span>
    <span style="color:#603000; ">QLCDNumber</span> <span style="color:#808030; ">*</span>disp<span style="color:#800080; ">;</span>             <span style="color:#696969; ">// Where to display the numbers</span>
    <span style="color:#603000; ">QPushButton</span> <span style="color:#808030; ">*</span>C<span style="color:#800080; ">;</span>             <span style="color:#696969; ">//creating the C button</span>
    <span style="color:#603000; ">QPushButton</span> <span style="color:#808030; ">*</span><span style="color:#603000; ">cos</span><span style="color:#800080; ">;</span>           <span style="color:#696969; ">//creating the consinus button</span>
    <span style="color:#603000; ">QPushButton</span> <span style="color:#808030; ">*</span><span style="color:#603000; ">sin</span><span style="color:#800080; ">;</span>           <span style="color:#696969; ">//creating the sinus button</span>

<span style="color:#800000; font-weight:bold; ">private</span><span style="color:#e34adc; ">:</span>
    <span style="color:#800000; font-weight:bold; ">int</span> <span style="color:#808030; ">*</span> left <span style="color:#808030; ">=</span><span style="color:#800000; font-weight:bold; ">nullptr</span><span style="color:#800080; ">;</span>          <span style="color:#696969; ">//left operand</span>
    <span style="color:#800000; font-weight:bold; ">int</span> <span style="color:#808030; ">*</span> right<span style="color:#808030; ">=</span><span style="color:#800000; font-weight:bold; ">nullptr</span><span style="color:#800080; ">;</span>         <span style="color:#696969; ">// right operand</span>
    <span style="color:#603000; ">QString</span> <span style="color:#808030; ">*</span>operation<span style="color:#808030; ">=</span><span style="color:#800000; font-weight:bold; ">nullptr</span><span style="color:#800080; ">;</span>  <span style="color:#696969; ">// Pointer on the current operation</span>

<span style="color:#800080; ">}</span><span style="color:#800080; ">;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">endif</span><span style="color:#004a43; "> </span><span style="color:#696969; ">// CALCULATOR_H</span>
</pre>

  
# Interaction des chiffres
L'idée de cette nouvelle connexion, c'est de connecter tous les boutons à ce slot. Cette fonction utilisera la Senderméthode pour obtenir l'identité du bouton sur lequel vous avez cliqué et agira en conséquence.

1.Par conséquent, nous allons ajouter les boutons de connexion et de connexion de tous les chiffres à cet emplacement.

     //Connecting the digits
     for(int i=0; i <10; i++)
         connect(digits[i], &QPushButton::clicked, 
                 this, &Calculator::newDigit);
                 
2.Maintenant, nous allons implémenter le newDigitslot pour afficher le chiffre dans le fichier LCDNumber.

      //Getting the identity of the button using dynamic_cast
      auto button  = dynamic_cast<QPushButton*>(sender());
     // Each button has his own digit in the text
     auto value = button->text()->toInt();
    //Displaying the digit
    disp->display(value);
  
Now each time, you will click on a button, his digit will be shown in the LCDNumber.  

# Integer numbers
Now that we can react to each digit, it is time to correctly implement the newDigit slot. We should clarify two points to clearly understand the implementation:

1.Which number, should be constructing left or right 

2.How to add digit to an existing number.

     *left = (*left) * 10 + digit
     
     
Here is the full implementation of this function using the mentioned details:

        void Calculator::newDigit( )
    {
        //getting the sender
        auto button = dynamic_cast<QPushButton*>(sender());
        //getting the value
        int value = button->text().toInt();
        //Check if we have an operation defined
        if(operation)
        {
            //check if we have a value or not
            if(!right)
                right = new int{value};
            else
                *right = 10 * (*right) + value;
            disp->display(*right);
        }
        else
        {
            if(!left)
                left = new int{value};
            else
                *left = 10 * (*left) + value;
            disp->display(*left);
        }
    }

# Operation Interaction
Now we will move on the operation of the four buttons. We will the same mechanism using the sender method. Hence we will define a single slot to handle the click on the operations buttons:

    public slots:
       void changeOperation();  //Slot to handle the click on operations
       void newDigit();
       
This slot will simply execute the following operations:

   *Get the identity of the sender button.
 
   *Store the clicked operation.
 
   *Reset the display to 0
 
 
     void Calculator::changeOperation()
     {
        //Getting the sender button
        auto button = dynamic_cast<QPushButton*>(sender());

        //Storing the operation
        operation = new QString{button->text()};

        //Initiating the right button
        right = new int{0};

        //reseting the display
        disp->display(0);
  }


# Enter Button
The final touch is left to you, You should implement the slot for the enter button to compute the result of combining the left and right value according to the operation.!!


# calculator.cpp

<pre style="color:#000000;background:#ffffff;"><span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">"</span><span style="color:#40015a; ">calculator.h</span><span style="color:#800000; ">"</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QKeyEvent</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QApplication</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QString</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QPushButton</span><span style="color:#800000; ">&gt;</span>

Calculator<span style="color:#800080; ">::</span>Calculator<span style="color:#808030; ">(</span><span style="color:#603000; ">QWidget</span> <span style="color:#808030; ">*</span>parent<span style="color:#808030; ">)</span>
    <span style="color:#800080; ">:</span> <span style="color:#603000; ">QWidget</span><span style="color:#808030; ">(</span>parent<span style="color:#808030; ">)</span>
<span style="color:#800080; ">{</span>
    createWidgets<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    placeWidget<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    makeConnexions<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    newDigit<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    changeOperation<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

<span style="color:#800080; ">}</span>


Calculator<span style="color:#800080; ">::</span><span style="color:#808030; ">~</span>Calculator<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span>
<span style="color:#800080; ">{</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> disp<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> layout<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> buttonsLayout<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> left <span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> right<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> operation<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> C<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> <span style="color:#603000; ">cos</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> <span style="color:#603000; ">sin</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> enter<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> CcossinLayout<span style="color:#800080; ">;</span>

<span style="color:#800080; ">}</span>


<span style="color:#800000; font-weight:bold; ">void</span> Calculator<span style="color:#800080; ">::</span>createWidgets<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span>
<span style="color:#800080; ">{</span>
    <span style="color:#696969; ">//Creating the layouts</span>
    layout <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QVBoxLayout</span><span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    layout<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setSpacing<span style="color:#808030; ">(</span><span style="color:#008c00; ">2</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>


    <span style="color:#696969; ">//creating the C, cos, sin Layout</span>
    CcossinLayout<span style="color:#808030; ">=</span><span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QHBoxLayout</span><span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    <span style="color:#696969; ">//grid layout</span>
    buttonsLayout <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QGridLayout</span><span style="color:#800080; ">;</span>


    <span style="color:#696969; ">//creating the buttons</span>
    <span style="color:#800000; font-weight:bold; ">for</span><span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">int</span> i<span style="color:#808030; ">=</span><span style="color:#008c00; ">0</span><span style="color:#800080; ">;</span> i <span style="color:#808030; ">&lt;</span> <span style="color:#008c00; ">10</span><span style="color:#800080; ">;</span> i<span style="color:#808030; ">+</span><span style="color:#808030; ">+</span><span style="color:#808030; ">)</span>
    <span style="color:#800080; ">{</span>
        digits<span style="color:#808030; ">.</span>push_back<span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QPushButton</span><span style="color:#808030; ">(</span><span style="color:#603000; ">QString</span><span style="color:#800080; ">::</span>number<span style="color:#808030; ">(</span>i<span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
        digits<span style="color:#808030; ">.</span>back<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setSizePolicy<span style="color:#808030; ">(</span><span style="color:#603000; ">QSizePolicy</span><span style="color:#800080; ">::</span>Expanding<span style="color:#808030; ">,</span> <span style="color:#603000; ">QSizePolicy</span><span style="color:#800080; ">::</span>Fixed<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
        digits<span style="color:#808030; ">.</span>back<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>resize<span style="color:#808030; ">(</span>sizeHint<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">.</span>width<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">,</span> sizeHint<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">.</span>height<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#800080; ">}</span>
    <span style="color:#696969; ">//enter button</span>
    enter <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QPushButton</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">Enter</span><span style="color:#800000; ">"</span><span style="color:#808030; ">,</span><span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    enter<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setSizePolicy<span style="color:#808030; ">(</span><span style="color:#603000; ">QSizePolicy</span><span style="color:#800080; ">::</span>Expanding<span style="color:#808030; ">,</span> <span style="color:#603000; ">QSizePolicy</span><span style="color:#800080; ">::</span>Fixed<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    enter<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>resize<span style="color:#808030; ">(</span>sizeHint<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">.</span>width<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">,</span> sizeHint<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">.</span>height<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    <span style="color:#696969; ">//operatiosn buttons</span>
    operations<span style="color:#808030; ">.</span>push_back<span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QPushButton</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">+</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    operations<span style="color:#808030; ">.</span>push_back<span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QPushButton</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">-</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    operations<span style="color:#808030; ">.</span>push_back<span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QPushButton</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">*</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    operations<span style="color:#808030; ">.</span>push_back<span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QPushButton</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">/</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>


    <span style="color:#696969; ">//creating the lcd</span>
    disp <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QLCDNumber</span><span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    disp<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setDigitCount<span style="color:#808030; ">(</span><span style="color:#008c00; ">6</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    <span style="color:#696969; ">//creating the C button</span>
    C<span style="color:#808030; ">=</span><span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QPushButton</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">C</span><span style="color:#800000; ">"</span><span style="color:#808030; ">,</span> <span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    <span style="color:#696969; ">//creating the cosinus button</span>
    <span style="color:#603000; ">cos</span> <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QPushButton</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">Cos</span><span style="color:#800000; ">"</span><span style="color:#808030; ">,</span> <span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>


    <span style="color:#696969; ">//creating the sinus button</span>
    <span style="color:#603000; ">sin</span> <span style="color:#808030; ">=</span><span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QPushButton</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">Sin</span><span style="color:#800000; ">"</span><span style="color:#808030; ">,</span> <span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

<span style="color:#800080; ">}</span>

<span style="color:#800000; font-weight:bold; ">void</span> Calculator<span style="color:#800080; ">::</span>placeWidget<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span>
<span style="color:#800080; ">{</span>

    layout<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addWidget<span style="color:#808030; ">(</span>disp<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    layout<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addLayout<span style="color:#808030; ">(</span>CcossinLayout<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    layout<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addLayout<span style="color:#808030; ">(</span>buttonsLayout<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

   <span style="color:#696969; ">//adding the C , cos , sin buttons</span>
    CcossinLayout<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addWidget<span style="color:#808030; ">(</span>C<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    CcossinLayout<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addWidget<span style="color:#808030; ">(</span><span style="color:#603000; ">cos</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    CcossinLayout<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addWidget<span style="color:#808030; ">(</span><span style="color:#603000; ">sin</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    <span style="color:#696969; ">//adding the buttons</span>
    <span style="color:#800000; font-weight:bold; ">for</span><span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">int</span> i<span style="color:#808030; ">=</span><span style="color:#008c00; ">1</span><span style="color:#800080; ">;</span> i <span style="color:#808030; ">&lt;</span><span style="color:#008c00; ">10</span><span style="color:#800080; ">;</span> i<span style="color:#808030; ">+</span><span style="color:#808030; ">+</span><span style="color:#808030; ">)</span>
        buttonsLayout<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addWidget<span style="color:#808030; ">(</span>digits<span style="color:#808030; ">[</span>i<span style="color:#808030; ">]</span><span style="color:#808030; ">,</span> <span style="color:#808030; ">(</span>i<span style="color:#808030; ">-</span><span style="color:#008c00; ">1</span><span style="color:#808030; ">)</span><span style="color:#808030; ">/</span><span style="color:#008c00; ">3</span><span style="color:#808030; ">,</span> <span style="color:#808030; ">(</span>i<span style="color:#808030; ">-</span><span style="color:#008c00; ">1</span><span style="color:#808030; ">)</span><span style="color:#808030; ">%</span><span style="color:#008c00; ">3</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>


    <span style="color:#696969; ">//Adding the operations</span>
    <span style="color:#800000; font-weight:bold; ">for</span><span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">int</span> i<span style="color:#808030; ">=</span><span style="color:#008c00; ">0</span><span style="color:#800080; ">;</span> i <span style="color:#808030; ">&lt;</span> <span style="color:#008c00; ">4</span><span style="color:#800080; ">;</span> i<span style="color:#808030; ">+</span><span style="color:#808030; ">+</span><span style="color:#808030; ">)</span>
        buttonsLayout<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addWidget<span style="color:#808030; ">(</span>operations<span style="color:#808030; ">[</span> i<span style="color:#808030; ">]</span><span style="color:#808030; ">,</span> i<span style="color:#808030; ">,</span> <span style="color:#008c00; ">4</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>


    <span style="color:#696969; ">//Adding the 0 button</span>
    buttonsLayout<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addWidget<span style="color:#808030; ">(</span>digits<span style="color:#808030; ">[</span><span style="color:#008c00; ">0</span><span style="color:#808030; ">]</span><span style="color:#808030; ">,</span> <span style="color:#008c00; ">3</span><span style="color:#808030; ">,</span> <span style="color:#008c00; ">0</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    buttonsLayout<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addWidget<span style="color:#808030; ">(</span>enter<span style="color:#808030; ">,</span> <span style="color:#008c00; ">3</span><span style="color:#808030; ">,</span> <span style="color:#008c00; ">1</span><span style="color:#808030; ">,</span> <span style="color:#008c00; ">1</span><span style="color:#808030; ">,</span><span style="color:#008c00; ">2</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    setLayout<span style="color:#808030; ">(</span>layout<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
<span style="color:#800080; ">}</span>

<span style="color:#800000; font-weight:bold; ">void</span> Calculator<span style="color:#800080; ">::</span>makeConnexions<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
    <span style="color:#696969; ">//Connecting the digits</span>
    <span style="color:#800000; font-weight:bold; ">for</span><span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">int</span> i<span style="color:#808030; ">=</span><span style="color:#008c00; ">0</span><span style="color:#800080; ">;</span> i <span style="color:#808030; ">&lt;</span><span style="color:#008c00; ">10</span><span style="color:#800080; ">;</span> i<span style="color:#808030; ">+</span><span style="color:#808030; ">+</span><span style="color:#808030; ">)</span>
        <span style="color:#400000; ">connect</span><span style="color:#808030; ">(</span>digits<span style="color:#808030; ">[</span>i<span style="color:#808030; ">]</span><span style="color:#808030; ">,</span> <span style="color:#808030; ">&amp;</span><span style="color:#603000; ">QPushButton</span><span style="color:#800080; ">::</span>clicked<span style="color:#808030; ">,</span>
                <span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">,</span> <span style="color:#808030; ">&amp;</span>Calculator<span style="color:#800080; ">::</span>newDigit<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>


<span style="color:#800080; ">}</span>

<span style="color:#800000; font-weight:bold; ">void</span> Calculator<span style="color:#800080; ">::</span>newDigit<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span>
<span style="color:#800080; ">{</span>

        <span style="color:#696969; ">//getting the sender</span>
        <span style="color:#603000; ">QPushButton</span> button <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">dynamic_cast</span><span style="color:#800080; ">&lt;</span><span style="color:#603000; ">QPushButton</span><span style="color:#800080; ">&gt;</span><span style="color:#808030; ">(</span>sender<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

        <span style="color:#696969; ">//getting the value</span>
        <span style="color:#800000; font-weight:bold; ">int</span> value <span style="color:#808030; ">=</span> button<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>text<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">.</span>toInt<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

        <span style="color:#696969; ">//Check if we have an operation defined</span>
        <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>operation<span style="color:#808030; ">)</span>
        <span style="color:#800080; ">{</span>
            <span style="color:#696969; ">//check if we have a value or not</span>
            <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span><span style="color:#808030; ">!</span>right<span style="color:#808030; ">)</span>
                right <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#800000; font-weight:bold; ">int</span><span style="color:#800080; ">{</span>value<span style="color:#800080; ">}</span><span style="color:#800080; ">;</span>
            <span style="color:#800000; font-weight:bold; ">else</span>
                <span style="color:#808030; ">*</span>right <span style="color:#808030; ">=</span> <span style="color:#008c00; ">10</span> <span style="color:#808030; ">*</span> <span style="color:#808030; ">(</span><span style="color:#808030; ">*</span>right<span style="color:#808030; ">)</span> <span style="color:#808030; ">+</span> value<span style="color:#800080; ">;</span>

            disp<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>display<span style="color:#808030; ">(</span><span style="color:#808030; ">*</span>right<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

        <span style="color:#800080; ">}</span>
        <span style="color:#800000; font-weight:bold; ">else</span>
        <span style="color:#800080; ">{</span>
            <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span><span style="color:#808030; ">!</span>left<span style="color:#808030; ">)</span>
                left <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#800000; font-weight:bold; ">int</span><span style="color:#800080; ">{</span>value<span style="color:#800080; ">}</span><span style="color:#800080; ">;</span>
            <span style="color:#800000; font-weight:bold; ">else</span>
                <span style="color:#808030; ">*</span>left <span style="color:#808030; ">=</span> <span style="color:#008c00; ">10</span> <span style="color:#808030; ">*</span> <span style="color:#808030; ">(</span><span style="color:#808030; ">*</span>left<span style="color:#808030; ">)</span> <span style="color:#808030; ">+</span> value<span style="color:#800080; ">;</span>

            disp<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>display<span style="color:#808030; ">(</span><span style="color:#808030; ">*</span>left<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
        <span style="color:#800080; ">}</span>



<span style="color:#800080; ">}</span>

<span style="color:#800000; font-weight:bold; ">void</span> Calculator<span style="color:#800080; ">::</span>changeOperation<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
    <span style="color:#696969; ">//Getting the sender button</span>
       <span style="color:#603000; ">QPushButton</span> button <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">dynamic_cast</span><span style="color:#800080; ">&lt;</span><span style="color:#603000; ">QPushButton</span><span style="color:#800080; ">&gt;</span><span style="color:#808030; ">(</span>sender<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

       <span style="color:#696969; ">//Storing the operation</span>
       operation <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QString</span><span style="color:#800080; ">{</span>button<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>text<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">}</span><span style="color:#800080; ">;</span>

       <span style="color:#696969; ">//Initiating the right button</span>
       right <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#800000; font-weight:bold; ">int</span><span style="color:#800080; ">{</span><span style="color:#008c00; ">0</span><span style="color:#800080; ">}</span><span style="color:#800080; ">;</span>

       <span style="color:#696969; ">//reseting the display</span>
       disp<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>display<span style="color:#808030; ">(</span><span style="color:#008c00; ">0</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
<span style="color:#800080; ">}</span>

<span style="color:#800000; font-weight:bold; ">void</span> Calculator<span style="color:#800080; ">::</span>keyPressEvent<span style="color:#808030; ">(</span><span style="color:#603000; ">QKeyEvent</span> <span style="color:#808030; ">*</span>e<span style="color:#808030; ">)</span>
<span style="color:#800080; ">{</span>
    <span style="color:#696969; ">//Exiting the application by a click on space</span>
    <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span> e<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>key<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#808030; ">=</span><span style="color:#808030; ">=</span> <span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span>Key_Escape<span style="color:#808030; ">)</span>
        qApp<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span><span style="color:#603000; ">exit</span><span style="color:#808030; ">(</span><span style="color:#008c00; ">0</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>


    <span style="color:#696969; ">//You could add more keyboard interation here (like digit to button)</span>
    <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>e<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>key<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">=</span><span style="color:#808030; ">=</span> <span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span>Key_0<span style="color:#808030; ">)</span>
        disp<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>display<span style="color:#808030; ">(</span><span style="color:#008c00; ">0</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">else</span> <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>e<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>key<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">=</span><span style="color:#808030; ">=</span> <span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span>Key_1<span style="color:#808030; ">)</span>
        disp<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>display<span style="color:#808030; ">(</span><span style="color:#008c00; ">1</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">else</span> <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>e<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>key<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">=</span><span style="color:#808030; ">=</span> <span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span>Key_2<span style="color:#808030; ">)</span>
        disp<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>display<span style="color:#808030; ">(</span><span style="color:#008c00; ">2</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">else</span> <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>e<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>key<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">=</span><span style="color:#808030; ">=</span> <span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span>Key_3<span style="color:#808030; ">)</span>
        disp<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>display<span style="color:#808030; ">(</span><span style="color:#008c00; ">3</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">else</span> <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>e<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>key<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">=</span><span style="color:#808030; ">=</span> <span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span>Key_4<span style="color:#808030; ">)</span>
        disp<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>display<span style="color:#808030; ">(</span><span style="color:#008c00; ">4</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">else</span> <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>e<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>key<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">=</span><span style="color:#808030; ">=</span> <span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span>Key_4<span style="color:#808030; ">)</span>
        disp<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>display<span style="color:#808030; ">(</span><span style="color:#008c00; ">4</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">else</span> <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>e<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>key<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">=</span><span style="color:#808030; ">=</span> <span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span>Key_5<span style="color:#808030; ">)</span>
        disp<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>display<span style="color:#808030; ">(</span><span style="color:#008c00; ">5</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">else</span> <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>e<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>key<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">=</span><span style="color:#808030; ">=</span> <span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span>Key_6<span style="color:#808030; ">)</span>
        disp<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>display<span style="color:#808030; ">(</span><span style="color:#008c00; ">6</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">else</span> <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>e<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>key<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">=</span><span style="color:#808030; ">=</span> <span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span>Key_7<span style="color:#808030; ">)</span>
        disp<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>display<span style="color:#808030; ">(</span><span style="color:#008c00; ">7</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">else</span> <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>e<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>key<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">=</span><span style="color:#808030; ">=</span> <span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span>Key_8<span style="color:#808030; ">)</span>
        disp<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>display<span style="color:#808030; ">(</span><span style="color:#008c00; ">8</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">else</span> <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>e<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>key<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">=</span><span style="color:#808030; ">=</span> <span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span>Key_9<span style="color:#808030; ">)</span>
        disp<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>display<span style="color:#808030; ">(</span><span style="color:#008c00; ">9</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>



<span style="color:#800080; ">}</span>
</pre>


![image](https://user-images.githubusercontent.com/86804863/142773713-8bc32ad3-6198-4fb2-8acf-a37cf1070d3b.png)












# Traffic Light
In this exercise, we will use the QTimer to simulate a traffic light.

( Simulating Traffic Light using Radio Buttons )

 1. Download the starter code TrafficLight.zip

 2. Investigate the code in order to underhand each component of the TrafficLight class.

 3. Your task is add some functions in order to change each 3 sedonds in the following order:

     Red -> Green -> Yellow


# header trafficlight.h

<pre style="color:#000000;background:#ffffff;"><span style="color:#004a43; ">#</span><span style="color:#004a43; ">ifndef</span><span style="color:#004a43; "> TRAFFIC_LIGHT_H</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">define</span><span style="color:#004a43; "> TRAFFIC_LIGHT_H</span>

<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QWidget</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QVector</span><span style="color:#800000; ">&gt;</span>
<span style="color:#800000; font-weight:bold; ">class</span> <span style="color:#603000; ">QRadioButton</span><span style="color:#800080; ">;</span>

<span style="color:#800000; font-weight:bold; ">class</span> TrafficLight<span style="color:#800080; ">:</span> <span style="color:#800000; font-weight:bold; ">public</span> <span style="color:#603000; ">QWidget</span><span style="color:#800080; ">{</span>
  <span style="color:#004a43; ">Q_OBJECT</span>

<span style="color:#800000; font-weight:bold; ">public</span><span style="color:#e34adc; ">:</span>

  TrafficLight<span style="color:#808030; ">(</span><span style="color:#603000; ">QWidget</span> <span style="color:#808030; ">*</span> parent <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">nullptr</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

<span style="color:#800000; font-weight:bold; ">protected</span><span style="color:#e34adc; ">:</span>
     <span style="color:#800000; font-weight:bold; ">void</span> createWidgets<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
     <span style="color:#800000; font-weight:bold; ">void</span> placeWidgets<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
     <span style="color:#696969; ">//---------------surcharger l'evenement--------------</span>
     <span style="color:#800000; font-weight:bold; ">void</span> timerEvent <span style="color:#808030; ">(</span><span style="color:#603000; ">QTimerEvent</span> <span style="color:#808030; ">*</span>e<span style="color:#808030; ">)</span>override<span style="color:#800080; ">;</span>
     <span style="color:#800000; font-weight:bold; ">void</span> keyPressEvent<span style="color:#808030; ">(</span><span style="color:#603000; ">QKeyEvent</span> <span style="color:#808030; ">*</span>e<span style="color:#808030; ">)</span>override<span style="color:#800080; ">;</span>


<span style="color:#800000; font-weight:bold; ">private</span><span style="color:#e34adc; ">:</span>
  <span style="color:#696969; ">//QVector &lt;QRadioButton *&gt; light;</span>
  <span style="color:#800000; font-weight:bold; ">int</span> index<span style="color:#808030; ">=</span><span style="color:#008c00; ">0</span><span style="color:#800080; ">;</span>
  <span style="color:#603000; ">QRadioButton</span> <span style="color:#808030; ">*</span> redlight<span style="color:#800080; ">;</span>
  <span style="color:#603000; ">QRadioButton</span> <span style="color:#808030; ">*</span> yellowlight<span style="color:#800080; ">;</span>
  <span style="color:#603000; ">QRadioButton</span> <span style="color:#808030; ">*</span> greenlight<span style="color:#800080; ">;</span>

  <span style="color:#696969; ">//variable</span>
  <span style="color:#800000; font-weight:bold; ">int</span> currentTime<span style="color:#800080; ">;</span>

<span style="color:#800080; ">}</span><span style="color:#800080; ">;</span>


<span style="color:#004a43; ">#</span><span style="color:#004a43; ">endif</span>
</pre>





# trafficlight.cpp

<pre style="color:#000000;background:#ffffff;"><span style="color:#004a43; ">&nbsp;&nbsp;&nbsp;</span><span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">"</span><span style="color:#40015a; ">trafficlight.h</span><span style="color:#800000; ">"</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QWidget</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QLayout</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QRadioButton</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QVector</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QKeyEvent</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QApplication</span><span style="color:#800000; ">&gt;</span>

TrafficLight<span style="color:#800080; ">::</span>TrafficLight<span style="color:#808030; ">(</span><span style="color:#603000; ">QWidget</span> <span style="color:#808030; ">*</span> parent<span style="color:#808030; ">)</span><span style="color:#800080; ">:</span> <span style="color:#603000; ">QWidget</span><span style="color:#808030; ">(</span>parent<span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>

    <span style="color:#696969; ">//Creatign the widgets</span>
    createWidgets<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    <span style="color:#696969; ">//place Widgets</span>
    placeWidgets<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>



    <span style="color:#696969; ">//timer</span>
    startTimer<span style="color:#808030; ">(</span><span style="color:#008c00; ">1000</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
<span style="color:#800080; ">}</span>

<span style="color:#800000; font-weight:bold; ">void</span> TrafficLight<span style="color:#800080; ">::</span>createWidgets<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span>
<span style="color:#800080; ">{</span>

  redlight <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QRadioButton</span><span style="color:#800080; ">;</span>
  redlight<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setEnabled<span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">false</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
  redlight<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>toggle<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
  redlight<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setStyleSheet<span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">QRadioButton::indicator:checked { background-color: red;}</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
  <span style="color:#696969; ">//light.append(redlight);</span>

  yellowlight <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QRadioButton</span><span style="color:#800080; ">;</span>
  yellowlight<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setEnabled<span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">false</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
  yellowlight<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setStyleSheet<span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">QRadioButton::indicator:checked { background-color: yellow;}</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
  <span style="color:#696969; ">//light.append(yellowlight);</span>

  greenlight <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QRadioButton</span><span style="color:#800080; ">;</span>
  greenlight<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setEnabled<span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">false</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
  greenlight<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setStyleSheet<span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">QRadioButton::indicator:checked { background-color: green;}</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
  <span style="color:#696969; ">//light.append(greenlight);</span>
<span style="color:#800080; ">}</span>


<span style="color:#800000; font-weight:bold; ">void</span> TrafficLight<span style="color:#800080; ">::</span>placeWidgets<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span>
<span style="color:#800080; ">{</span>

  <span style="color:#696969; ">// Placing the widgets</span>
  <span style="color:#800000; font-weight:bold; ">auto</span> layout <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QVBoxLayout</span><span style="color:#800080; ">;</span>
  layout<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addWidget<span style="color:#808030; ">(</span>redlight<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
  layout<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addWidget<span style="color:#808030; ">(</span>yellowlight<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
  layout<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addWidget<span style="color:#808030; ">(</span>greenlight<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
  setLayout<span style="color:#808030; ">(</span>layout<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
<span style="color:#800080; ">}</span>

<span style="color:#800000; font-weight:bold; ">void</span> TrafficLight<span style="color:#800080; ">::</span>timerEvent<span style="color:#808030; ">(</span><span style="color:#603000; ">QTimerEvent</span> <span style="color:#808030; ">*</span>e<span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
<span style="color:#696969; ">//    index = (index +1)%3;</span>
<span style="color:#696969; ">//    light [index]-&gt; toggle();</span>

 <span style="color:#696969; ">//-----------------------------------------------------------</span>
    <span style="color:#696969; ">//si le rouge est active==&gt;active le yellow</span>
    <span style="color:#696969; ">// if(redlight-&gt;isChecked())</span>
     <span style="color:#696969; ">//   yellowlight-&gt;toggle();</span>


    <span style="color:#696969; ">//si le yellow est active ==&gt;active le green</span>
    <span style="color:#696969; ">//else if(yellowlight-&gt;isChecked())</span>
     <span style="color:#696969; ">//   greenlight-&gt;toggle();</span>


    <span style="color:#696969; ">//si le green est active  ==&gt;active le rouge</span>
    <span style="color:#696969; ">//else if(greenlight-&gt;isChecked())</span>
    <span style="color:#696969; ">//    redlight-&gt;toggle();</span>
  <span style="color:#696969; ">//----------------------------------------------------------</span>
    <span style="color:#696969; ">//incrementer le temps courant du feux</span>
    currentTime<span style="color:#808030; ">+</span><span style="color:#808030; ">+</span><span style="color:#800080; ">;</span>

    <span style="color:#696969; ">//verifier si  je dois passer du rouge au faune</span>
    <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>redlight<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>isChecked<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">&amp;</span><span style="color:#808030; ">&amp;</span> currentTime<span style="color:#808030; ">=</span><span style="color:#808030; ">=</span><span style="color:#008c00; ">4</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
        yellowlight<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>toggle<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
        currentTime<span style="color:#808030; ">=</span><span style="color:#008c00; ">0</span><span style="color:#800080; ">;</span>

    <span style="color:#800080; ">}</span>
    <span style="color:#696969; ">//verifier si je dois passer du jaune au vert</span>
    <span style="color:#800000; font-weight:bold; ">else</span> <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>yellowlight<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>isChecked<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#808030; ">&amp;</span><span style="color:#808030; ">&amp;</span> currentTime<span style="color:#808030; ">=</span><span style="color:#808030; ">=</span><span style="color:#008c00; ">1</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
        greenlight<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>toggle<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
        currentTime<span style="color:#808030; ">=</span><span style="color:#008c00; ">0</span><span style="color:#800080; ">;</span>
    <span style="color:#800080; ">}</span>

    <span style="color:#696969; ">//verifier si je dois passer du vert au rouge</span>
    <span style="color:#800000; font-weight:bold; ">else</span> <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>greenlight<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>isChecked<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#808030; ">&amp;</span><span style="color:#808030; ">&amp;</span> currentTime<span style="color:#808030; ">=</span><span style="color:#808030; ">=</span><span style="color:#008c00; ">2</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
        redlight<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>toggle<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
        currentTime<span style="color:#808030; ">=</span><span style="color:#008c00; ">0</span><span style="color:#800080; ">;</span>
    <span style="color:#800080; ">}</span>

<span style="color:#800080; ">}</span>
<span style="color:#800000; font-weight:bold; ">void</span> TrafficLight<span style="color:#800080; ">::</span>keyPressEvent<span style="color:#808030; ">(</span><span style="color:#603000; ">QKeyEvent</span> <span style="color:#808030; ">*</span>e<span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
<span style="color:#696969; ">//    if (e-&gt;key() ==Qt::Key_Escape)</span>
<span style="color:#696969; ">//        qApp-&gt;exit();</span>
<span style="color:#696969; ">//    if( e-&gt;key() ==Qt::Key_R){</span>
<span style="color:#696969; ">//        index=0;  //hidden state</span>
<span style="color:#696969; ">//        light[index]-&gt;toggle();</span>
<span style="color:#696969; ">//    }</span>
<span style="color:#696969; ">//    else if( e-&gt;key() ==Qt::Key_Y){</span>
<span style="color:#696969; ">//        index =1;</span>
<span style="color:#696969; ">//        light[index]-&gt;toggle();</span>
<span style="color:#696969; ">//    }</span>
<span style="color:#696969; ">//    else if( e-&gt;key() ==Qt::Key_G){</span>
<span style="color:#696969; ">//        index=2;</span>
<span style="color:#696969; ">//        light[index]-&gt;toggle();</span>
<span style="color:#696969; ">//    }</span>
    <span style="color:#696969; ">//-------------------------------------------</span>
        <span style="color:#800000; font-weight:bold; ">if</span> <span style="color:#808030; ">(</span>e<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>key<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#808030; ">=</span><span style="color:#808030; ">=</span><span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span>Key_Escape<span style="color:#808030; ">)</span>
            qApp<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span><span style="color:#603000; ">exit</span><span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
        <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span> e<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>key<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#808030; ">=</span><span style="color:#808030; ">=</span><span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span>Key_R<span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
             <span style="color:#696969; ">//hidden state</span>
            <span style="color:#696969; ">//index=0</span>
            <span style="color:#696969; ">//light[index]-&gt;toggle();</span>
            redlight<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>toggle<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
        <span style="color:#800080; ">}</span>
        <span style="color:#800000; font-weight:bold; ">else</span> <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span> e<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>key<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#808030; ">=</span><span style="color:#808030; ">=</span><span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span>Key_Y<span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
<span style="color:#696969; ">//            index =1;</span>
<span style="color:#696969; ">//            light[index]-&gt;toggle();</span>
            yellowlight<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>toggle<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
        <span style="color:#800080; ">}</span>
        <span style="color:#800000; font-weight:bold; ">else</span> <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span> e<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>key<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#808030; ">=</span><span style="color:#808030; ">=</span><span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span>Key_G<span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
<span style="color:#696969; ">//            index=2;</span>
<span style="color:#696969; ">//            light[index]-&gt;toggle();</span>
            greenlight<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>toggle<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
        <span style="color:#800080; ">}</span>




<span style="color:#800080; ">}</span> 
</pre>


![image](https://user-images.githubusercontent.com/86804863/142775137-3ee8b6f3-c54f-4a23-9d42-d5e1562f5834.png)












