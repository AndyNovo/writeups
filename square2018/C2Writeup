# Square CTF 2018

## Challenge 2 Write-Up: Flipping Bits

In RSA problems you can win many ways:

* Factoring the modulus
* The inverse of the public exponent modulo phi(modulus) == (p-1)*(q-1)
* Poorly Set Parameters (like p and q being very close to each other)
* A small message so that m^e is smaller than the modulus

In this case we have two cipher texts one is m1^e1 % N the other is m2^e2 % N
and e2 = 15 and e1 = 13.  But we have the additional knowledge that
e2 was supposed to be e1.  So there might not be a modular inverse of e2.

At first I lost time looking for RSA exploits with small close exponents or
what goes wrong when the wrong exponent is used in RSA and had no luck.

In the process I went looking for algebraic relationships between e1*e2 and N
or Phi.  Maybe e2*d would have something interesting going on that could lead
to an exploit.

Then, after some frustration, I recognized that they didn't specify that m1
wasn't the same as m2 and if it were then inverting the first cipher text will
get me ct1^(-1) == m1^(-e1).  Multiplying by m1^(e1 + 2) would give m1^(e1 + 2 - e1)
which might be a small enough message/exponent combo that we can just take a square root.

Sure enough long_to_bytes(sqrt(inverse_mod(ct1, modulus)*ct2)) reveals the message.

I switched to cloud.sagemath.com to get the large integer exact squareroot.

Here is my solve.sagews code:

from Crypto.Util.number import *
N=103109065902334620226101162008793963504256027939117020091876799039690801944735604259018655534860183205031069083254290258577291605287053538752280231959857465853228851714786887294961873006234153079187216285516823832102424110934062954272346111907571393964363630079343598511602013316604641904852018969178919051627
ct1=13981765388145083997703333682243956434148306954774120760845671024723583618341148528952063316653588928138430524040717841543528568326674293677228449651281422762216853098529425814740156575513620513245005576508982103360592761380293006244528169193632346512170599896471850340765607466109228426538780591853882736654
ct2=79459949016924442856959059325390894723232586275925931898929445938338123216278271333902062872565058205136627757713051954083968874644581902371182266588247653857616029881453100387797111559677392017415298580136496204898016797180386402171968931958365160589774450964944023720256848731202333789801071962338635072065
long_to_bytes(sqrt((inverse_mod(ct1, N)*ct2) % N))
