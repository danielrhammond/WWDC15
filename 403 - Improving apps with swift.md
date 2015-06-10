Improving existing apps with Swift (403)

# Getting rid of global utility functions
Encapsulate global utility function and turn them into struct methods
	CGRect:		CGRectZero()		CGRectMake() 	CGRectGetMaxY()
						.zeroRect			init(x:…) 		.maxY

# Availability
Gives compile time feedback on mismatch between deployment targets and APIs being used

# 