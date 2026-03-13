# Linear-Block-Code
# Aim
Write a simple python program to Generate Matrix, Codeword, Hamming weight, Syndrome matrix and find the error on received codeword using Linear block code. 
# Tools required
Python-IDE
# Program
```
import numpy as np

r = int(input("Enter the Parity bits : "))
k = int(input("Enter the Message bits : "))

P = np.array([list(map(int, input(f"Enter row {i+1} (space separated) : ").split())) for i in range(k)])
G = np.hstack((P, np.eye(k, dtype=int)))
print("\nGenerator Matrix (G):")
for i in G: print(*i)

n = G.shape[1]
msg = np.array([[int(b) for b in format(i,f'0{k}b')] for i in range(2**k)])
cw = np.mod(msg @ G, 2)

print("\nMessage   Codeword   Weight")
wt = []
for m,c in zip(msg,cw):
    w = np.sum(c); wt.append(w)
    print(*m,"   ",*c,"   ",w)

print("\nMinimum Hamming Distance:",min([i for i in wt if i!=0]))
H = np.hstack((np.eye(r,dtype=int),P.T))
print("\nParity Check Matrix (H):")
for i in H: print(*i)
rc = np.array(list(map(int,input("\nEnter the received codeword : ").split())))
S = np.mod(rc @ H.T,2)
print("Syndrome :",*S)
e = np.zeros(n,dtype=int)
for i in range(n):
    if np.array_equal(H.T[i],S): e[i]=1

print("Error Vector :",*e)
print("Corrected Codeword :",*(np.mod(rc+e,2)))
```
# Output Waveform
<img width="300" height="500" alt="Screenshot (302)" src="https://github.com/user-attachments/assets/eae8a4d8-44f5-4f78-b151-69f7f4d120ff" />

# Results
Thus linear block code operation for the given input is successfully verified.
