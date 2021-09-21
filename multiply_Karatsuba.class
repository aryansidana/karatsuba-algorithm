	public HugeInteger multiply(HugeInteger h) {
		HugeInteger prod = new HugeInteger();
		int n;
		int size1 = this.length;
		int size2 = h.length;
		int carry=0;
	
		
		/*
		if(size1!=size2) {
			if (size1>size2) {
				if(size1%2==0&size2%2==0) {
					carry=size1-size2;
					HugeInteger h2 = new HugeInteger(h.length+(size1-size2));
					h2.length=h.length+(size1-size2);
					int count=h2.length-1;
					for(int i=0; i<h2.length;i++) {
						if (i<h.length) 
							h2.data[count]=h.data[h.length-i-1];
						else
							h2.data[count]=0;
						count--;	
					}
					prod=this.multiply_Karatsuba(h2);
					prod.remove=carry;
					return prod;
				}
				if(size1%2==1&size2%2==1) {
					carry=size1-size2+1;
					HugeInteger h1 = new HugeInteger(this.length+1);
					HugeInteger h2 = new HugeInteger(h.length+(size1-size2)+1);
					h2.length=h.length+(size1-size2)+1;
					h1.length=this.length+1;
					int count=h2.length-1;
					for(int i=0; i<h2.length;i++) {
						if (i<h.length) 
							h2.data[count]=h.data[h.length-i-1];
						else
							h2.data[count]=0;
						count--;	
					}
					count=h1.length-1;
					for(int i=0; i<h1.length;i++) {
						if (i<this.length) 
							h1.data[count]=this.data[this.length-i-1];
						else
							h1.data[count]=0;
						count--;	
					}
					
					prod=h1.multiply_Karatsuba(h2);
					prod.remove=carry;
					return prod;
				}
			}
		}
		 	
		else*/
		
		prod=this.multiply_Karatsuba(h);
		
		if (this.negative==true&h.negative==true)
			prod.negative=false;
		else if (this.negative==true) {
			prod.negative=true;
		}
		else if (h.negative==true) {
			prod.negative=true;
		}
		else
			prod.negative=false;
		if(prod.length==1&prod.data[0]==0)
			prod.negative=false;
		
		return prod;
	}
	public HugeInteger multiply_Karatsuba(HugeInteger h) {
		HugeInteger prod = new HugeInteger();
		int n;
		int size1 = this.length;
		int size2 = h.length;
		
		
		if(size1==size2&size1==1) {
			prod = new HugeInteger(1);
			prod.length=1;
			prod.data[0]=this.data[0]*h.data[0];
			if(prod.data[0]>9) {
				prod = new HugeInteger(2);
				prod.length=2;
				prod.data[0]=(this.data[0]*h.data[0])%10;
				prod.data[1]=((this.data[0]*h.data[0])-prod.data[0])/10;

			}
			
			else if (prod.data[0]<0){
				prod.negative=true;
				prod.data[0]*=-1;
			}
			return prod;
		}
		
		if (h.length>this.length) 
			n=h.length;
		
		else
			n=this.length;
		System.out.println();
		System.out.println("New Call");
		
		n = (n/2)+(n%2);
		if (size2>size1&size2%2==1)
			n--;
		System.out.println("DIV: "+n+"\n");
		System.out.println(this.toString());
		System.out.println(h.toString());
		HugeInteger a = this.shiftL(n);
		System.out.println("a: "+a);
		HugeInteger b = this.shiftR(n);
		System.out.println("b: "+b);
		HugeInteger c = h.shiftL(n);
		System.out.println("c: "+c);
		HugeInteger d = h.shiftR(n);
		System.out.println("d: "+d);
		HugeInteger ac = a.multiply_Karatsuba(c);
		System.out.println("ac: "+ac);
		HugeInteger bd = b.multiply_Karatsuba(d);
		//System.out.println("acL: "+ac.length);
		System.out.println("bd: "+bd);
		
	
		HugeInteger abcd = ((a.add(b)).multiply_Karatsuba((c.add(d))));
		//System.out.println("a+b: "+(a.add(b)));
		//System.out.println("c+d: "+(c.add(d)));
		//System.out.println((a.add(b)).multiply((c.add(d))));
		System.out.println("abcd: "+abcd);
		//System.out.println("sub1: "+(abcd.subtract(bd)).toString());
		//HugeInteger sub1 =(abcd.subtract(bd));
		//System.out.println("sub2: "+(sub1.subtract(ac)).toString());
		//System.out.println("sub2ac: "+ac.toString());
		//System.out.println("sub2acL: "+ac.length);
		HugeInteger sub = abcd.subtract(bd).subtract(ac);
		System.out.println("sub: "+sub);
	    System.out.println("sub: "+sub+" = "+abcd+" - "+bd+" - "+ac);
		System.out.println("N: "+n+"\n");
		System.out.println("Results: "+((ac.shift(n*2)).add(bd).add(sub.shift(n))).toString());
		System.out.println("Result: "+((ac.shift(n*2)).add(bd).add(sub.shift(n))).toString()+" = "+(ac.shift(n*2))+" + "+bd+" + "+(sub.shift(n)));
		//System.out.println("ResultsL: "+((ac.shift(n*2)).add(bd).add(sub.shift(n))).length);
		//System.out.println("Results0: "+((ac.shift(n*2)).add(bd).add(sub.shift(n))).data[2]);
		//System.out.println("N: "+n);
		//System.out.println();
		return (ac.shift(n*2)).add(bd).add(sub.shift(n));
		
	}
	
	public HugeInteger shift(int n) {
		if(this.length==1&this.data[0]==0) {
			HugeInteger shift=new HugeInteger(1);
			shift.length=1;
			shift.data[0]=0;
			return shift;
		}
		HugeInteger shift=new HugeInteger(this.length+n);
		shift.length=this.length+n;
		int count=shift.length-1;
		for(int i=0;i<shift.length;i++) {
			if(i<this.length) 
				shift.data[count]=this.data[this.length-i-1];
			else
				shift.data[count]=0;
			count--;
		}
		
		return shift;
	}
	
	public HugeInteger shiftL(int n) {
		if(n>1&this.length%2==1)
			n--;
		//System.out.println("LengthL: "+(this.length-n));
		if(this.length-n<0||(this.length==1&n==1)) {
			HugeInteger shift=new HugeInteger(1);
			shift.length=1;
			shift.data[0]=0;
			return shift;
		}
		if(this.length==n)
			n--;
		n++;
		HugeInteger shift=new HugeInteger(this.length-n+1);
		shift.length=n-1;
		int count = shift.length-1;
		for (int i=0;i<n-1;i++) {
			shift.data[count]=this.data[this.length-i-1];
			count--;
		}
		//System.out.println("Lshift: " +shift.toString());
		return shift;
		
	}
	
	public HugeInteger shiftR(int n) {
		
		if(n>1&this.length%2==1)
			n--;
		//System.out.println("LengthR: "+(this.length-n));
		if(this.length-n<=0) {
			HugeInteger shift=new HugeInteger(1);
			shift.length=1;
			shift.data[0]=this.data[0];
			return shift;
		}
		
		HugeInteger shift=new HugeInteger(this.length-n);
		shift.length=this.length-n;
		//if(n==1&this.length>2)
			//n++;
		//if(n==2&this.length>4)
			//n++;
		if(this.length>n+n)
			n++;
		if(this.length>n+n)
			n++;
		for (int i=0;i<n;i++) {
			shift.data[i]=this.data[i];
			
		}
		//System.out.println("Rshift: " +shift.toString());
		return shift;
		
	}
	