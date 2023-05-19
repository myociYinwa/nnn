## How to Implement a Shift Register Parallel In Serial Out in VHDL

 
![Shift Register Parallel In Serial Out Vhdl Code Fix](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT1y4k2xqVxnszqanhX5eDq4-scpt53V5Iwa0BJhaYuttfh_6debdi56-c)

 
# How to Implement a Shift Register Parallel In Serial Out in VHDL
 
A shift register parallel in serial out (PISO) is a type of shift register that allows multiple bits of data to be entered in parallel and then shifted out sequentially. This can be useful for converting parallel data to serial data for communication or storage purposes. In this article, we will show how to implement a PISO shift register in VHDL using a generic parameter for the number of bits and a simple state machine for the shifting logic.
 
## shift register parallel in serial out vhdl code


[**Download Zip**](https://www.google.com/url?q=https%3A%2F%2Ftiurll.com%2F2tLkxD&sa=D&sntz=1&usg=AOvVaw0E4zrcJ8l7Iq6N3kwHJLG2)

 
## Shift Register Parallel In Serial Out Circuit
 
A PISO shift register consists of a set of D flip-flops that store the parallel input data and a multiplexer that selects between the parallel input and the serial output of the previous flip-flop. The following figure shows a four-bit PISO shift register circuit.
 ![PISO circuit](https://i.stack.imgur.com/0nq3T.png) 
The parallel input data is loaded into the flip-flops when the load signal is high. When the load signal is low, the enable signal controls the shifting operation. When the enable signal is high, the flip-flops are clocked and the data is shifted out from the least significant bit (LSB) to the most significant bit (MSB). The serial output data is available at the s\_out port.
 
## Shift Register Parallel In Serial Out VHDL Code
 
To implement a PISO shift register in VHDL, we can use a generic parameter to specify the number of bits and a signal to store the intermediate data. We can also use an enumeration type to define the possible states of the shift register: waiting and shifting. The waiting state is when the load signal is high and the shifting state is when the load signal is low and the enable signal is high. The following VHDL code shows a possible implementation of a PISO shift register.

    library ieee;
    use ieee.std_logic_1164.all;
    
    entity piso is
      generic (
        n : integer := 4 -- number of bits
      );
      port (
        clk : in std_logic; -- clock
        reset : in std_logic; -- reset
        load : in std_logic; -- load parallel input
        parallel_in : in std_logic_vector (n-1 downto 0); -- parallel input
        s_in : in std_logic; -- serial input
        s_out : out std_logic -- serial output
      );
    end piso;
    
    architecture behavioral of piso is
    
      -- intermediate data
      signal temp_reg : std_logic_vector (n-1 downto 0) := (others => '0');
      
      -- possible states
      type possible_states is (waiting, shifting);
      
      -- current state
      signal state : possible_states := waiting;
      
      -- shift counter
      signal shift_counter : integer range 0 to n-1 := 0;
      
    begin
    
      process (clk, reset)
      begin
        if reset = '1' then -- reset state
          temp_reg <= (others => '0'); -- clear intermediate data
          state <= waiting; -- go to waiting state
          shift_counter <= 0; -- reset shift counter
          s_out <= '0'; -- clear serial output
        elsif clk'event and clk = '1' then -- rising clock edge
          case state is 
            when waiting => -- waiting state
              if load = '1' then -- load parallel input
                temp_reg <= parallel_in; -- store parallel input
                s_out <= '0'; -- clear serial output
              else -- start shifting
                state <= shifting; -- go to shifting state
                shift_counter <= 0; -- reset shift counter
              end if;
            when shifting => -- shifting state
              if enable = '1' then -- shift enabled
                if shift_counter < n-1 then -- not done yet
                  s_out <= temp_reg(0); -- output LSB
                  temp_reg <= s_in & temp_reg(n-1 downto 1); -- shift right with serial input
                  shift_counter <= shift_counter + 1; -- increment shift counter
                else -- done shifting
                  s_out <= temp_reg(0); -- output LSB
                  temp_reg <= (others => '0 0f148eb4a0
