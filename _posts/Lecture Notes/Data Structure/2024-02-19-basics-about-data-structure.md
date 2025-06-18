---  
tags:  
  - data-structure  
  - memory  
  - allocation  
share: "true"  
github_title: 2024-02-19-basics-about-data-structure  
title: 0. Basics about Data Structure  
date: 2024-02-19  
categories:  
  - Lecture Notes  
  - Data Structure  
---  
  
# Basic forms of Allocation  
  
**We can classify memory allocation as either**  
- Contiguous  
- Linked  
- Indexed  
  
> Q. Storage allocation === Memory Allocation?  
> A. Storage is non-volatile(address a block), while memory is volatile(unit of byte); we need different design.  
  
  
## Contiguous Allocation  
  
- An array stores 'n' objects in a contiguous space of memory.  
- We have to `copy all information to new memory` when the additional memory is required.  
  
  
## Linked Allocation  
  
- Linked storage associates two piece of data, with each item being stored:  
	- the datum itself, and  
	- a reference to the next item!  
	  
  
You have to read all the blocks through the whole data structure.(which you don't have to do in contiguous allocation.)  
  
This is an example for linked allocation.  
```  
template <typename Type>  
class Node {  
	private:  
		Type node_value;  
		Node *next_node;  
	public:  
	 // ...  
}  
```  
  
## Indexed Allocation  
  
With indexed allocation, an array of pointers link to allocated memory locations.  
Each pointers link to some data (possibly NULL).  
  
  
