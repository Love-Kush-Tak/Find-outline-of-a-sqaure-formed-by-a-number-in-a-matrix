# Find-outline-of-a-sqaure-formed-by-a-number-in-a-matrix
You are given a matrix of dimensions M*N. Find out whether there is an outline of a square formed by the number 4 in the matrix of numbers.
Input Description:
Dimensions of the matrix followed followed by the elements of the matrix.

Output Description:
YES/NO

Sample Input :
5 5
4 4 4 4 4
4 1 2 3 4
4 7 6 5 4
4 9 8 7 4
4 4 4 4 4
Sample Output :
YES
* ** * ** * * ** * * ** * * * ** * ** * * * * ** * ** *** * * * **  ** * * * ** * *  * * ** * * * * * ** * * * ** * * * ** * * * ** * * * 
# consider a square having lest most corner as D, then immediate right corner of it as A, then bottom one to A as B, and at left to B as C 
Basic fundae used:
1) strart scanning each element row wise and look if it has 4 in it
2) then we look if it has 4 in its right too, if we get 4 at its right we look at the immediate bottom and look if it has also 4 there
3) if there is again 4 at the bottom we look at the immediate left and look if it has 4 there
4) if there is again a 4 at the left we look at the top if there is a 4 there too
5 In 2nd, 3rd, 4th step we keep in mic=nd that number of 4 are same otherwise we will not have a sqaure
6) If we donot find a 4 in 2nd, 3rd, 4th step then we break the loop at that time and again start looking for 4 from 1st step
7) repeat above steps, if a square is formed we print YES otherwise NO
Code in python:
# For taking size of array as an input
MN = list(map(int, input().split()))
m =MN[0]
n = MN[1]
matrix = []
# For taking the elements as input
for i in range(m):
  arr = list(map(int, input().split()))
  matrix.append(arr)
i = 0
num = 0
#num says even if we find one outline we will increase the num by 1 and print "YES" and if num remains zero over the full cycle 
length_1 = 0
length_2 = 0
length_3 = 0
length_4 = 0
while(i !=m):
  j = 0
  length_1 = 0
  #From D to A
  while(j != n):
    times = 1
    if(matrix[i][j] == 4):
      length_1 += 1 
      if(length_1 >times):
        #COORDINATES OF A
        i_A = i
        j_A = j
        ##COORDINATES OF D
        i_D = i
        j_D = j-length_1 + 1
        i_ = i_A
        #print(length_1, i_A, j_A, i_D, j_D)
        length_2 = 0
        times += 1
        # From A to B
        while(i_!=i_A+length_1):
          i_ += 1
          if(matrix[i_-1][j] == 4):
            length_2 += 1
            #print(length_2)
            if(length_2 != length_1 and i_ == i_A+length_1):
              break
            elif(length_2 == length_1):
              i_B = i_ -1  
              j_B = j
              #print(i_B, j_B, i_A, j_A)  
              # From B to C
              length_3 = 0
              while(j != j_D-1):
                j-=1
                if(matrix[i_-1][j+1]==4):
                  length_3 += 1
                  #print(length_3)
                  if(length_3 != length_1 and j == j_D-1):
                    break 
                  elif(length_3 == length_1):
                    i_C = i_ -1
                    j_C = j +1
                    length_4 = 0
                    while(i_ -1!= i_D-1):
                      i_ -= 1
                      if(matrix[i_][j+1]==4):
                        length_4 += 1
                        #print(length_4)
                        if(length_4 != length_1 and i_ -1 == i_D-1 ):
                          break
                        elif(length_4==length_1):
                          print("YES")
                          num += 1
                          break
                    if(length_4==length_1):
                      break
              if(length_4==length_1):
                break

          else: break
        if(length_4==length_1):
          break       
      
    else:
      length_1 = 0
      
    j += 1
  if(length_4==length_1):
    break  

  i+=1
if(num == 0):
  print("NO")
