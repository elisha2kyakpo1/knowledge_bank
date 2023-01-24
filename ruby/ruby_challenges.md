# Interview questions

## Binary search

```Ruby
def binary_search(array, value, left, right)
  # If the left index is greater than the right index, the value was not found
  if left > right
    return -1
  end
  # Calculate the midpoint
  mid = (left + right) / 2
  # If the value is less than the element at the midpoint, search the left half
  if value < array[mid]
    binary_search(array, value, left, mid - 1)
  # If the value is greater than the element at the midpoint, search the right half
  elsif value > array[mid]
    binary_search(array, value, mid + 1, right)
  # If the value is equal to the element at the midpoint, return the index
  else
    return mid
  end
end
```

This function performs a binary search to find the index of a given value in a sorted array. It takes four arguments: the array to search, the value to search for, and the left and right indices defining the search interval.

The function first checks if the left index is greater than the right index. If it is, it means that the value was not found in the array and the function returns -1.

If the left index is not greater than the right index, the function calculates the midpoint of the search interval. It then checks if the value is less than, greater than, or equal to the element at the midpoint of the interval.

If the value is less than the element at the midpoint, the function calls itself with the left half of the interval as the new search interval. If the value is greater than the element at the midpoint, the function calls itself with the right half of the interval as the new search interval. If the value is equal to the element at the midpoint, the function returns the index of the element.

This process continues until the value is found or the left index becomes greater than the right index, at which point the function returns -1 or the index of the value.

## Two_sum challenge

```Ruby
def two_sum(nums, target)
  # Create a hash map to store the indices of each element
  index_map = {}
  # Create an array to store the pairs of indices
  pairs = []
  nums.each_with_index do |num, i|
    # Calculate the complement (the number we need to add to `num`
    # to get the target)
    complement = target - num
    # If the complement is in the hash map, add the indices to the
    # pairs array
    if index_map[complement]
      pairs << [index_map[complement], i]
    end
    # Add the current element and its index to the hash map
    index_map[num] = i
  end
  # Return the pairs array
  pairs
end
```

It creates an empty hash map called index_map and an empty array called pairs. These will be used to store the indices of the elements and the pairs of indices that add up to the target, respectively.
It iterates through the nums array using the each_with_index method. This method allows the function to access the current element and its index as it iterates through the array.
For each element num and its index i, it calculates the complement (the number that needs to be added to num to get the target). For example, if the target is 9 and the current element is 2, the complement would be 7 (9 - 2 = 7).
It checks if the complement is in the index_map hash map. If it is, it means that an element with that value has already been seen, and the indices of the element and the complement can be added to the pairs array. For example, if the target is 9 and the current element is 2, and an element with a value of 7 has already been seen and added to the index_map hash map, the indices of the 2 and the 7 can be added to the pairs array.
Regardless of whether the complement was found in the index_map hash map, the current element and its index are added to the `.

## Fibonacci

```Ruby
def fibonacci(n)
  if n == 0
    0
  elsif n == 1
    1
  else
    fibonacci(n - 1) + fibonacci(n - 2)
  end
end

puts fibonacci(6)  # Output: 8
```

This function calculates the nth number in the Fibonacci sequence, which is a series of numbers in which each number is the sum of the two preceding ones, usually starting with 0 and 1.

The function has three parts:

A base case: if n is 0, the function returns 0.
A base case: if n is 1, the function returns 1.
A recursive case: if n is neither 0 nor 1, the function calls itself with n - 1 and n - 2 as arguments, and adds the results together.
For example, if the function is called with an argument of 6, it will call itself with arguments of 5 and 4, which will call themselves with arguments of 4 and 3 and 3 and 2, respectively. This will continue until the base cases are reached and the function starts returning. The final result will be the sum of all the returned values, which is the 6th number in the Fibonacci sequence.

## Linked list

```Ruby
class LinkedList
  # A linked list node has a value and a link to the next node
  class Node
    attr_accessor :value, :next

    def initialize(value, next_node=nil)
      @value = value
      @next = next_node
    end
  end

  # The linked list has a head (the first node) and a tail (the last node)
  attr_accessor :head, :tail

  def initialize
    @head = nil
    @tail = nil
  end

  # Add a value to the end of the list
  def append(value)
    new_node = Node.new(value)
    if @head.nil?
      @head = new_node
      @tail = new_node
    else
      @tail.next = new_node
      @tail = new_node
    end
  end

  # Remove the last element from the list
  def pop
    return nil if @head.nil?
    current_node = @head
    previous_node = nil
    while current_node.next
      previous_node = current_node
      current_node = current_node.next
    end
    previous_node.next = nil
    @tail = previous_node
    current_node.value
  end

  # Find the index of a value in the list
  def find(value)
    current_node = @head
    index = 0
    while current_node
      return index if current_node.value == value
      current_node = current_node.next
      index += 1
    end
    nil
  end

  # Insert a value at a specific index
  def insert(value, index)
    new_node = Node.new(value)
    if index == 0
      new_node.next = @head
      @head = new_node
```

The linked list class has a nested Node class, which represents a single node in the linked list. Each node has a value and a next attribute, which stores the node's value and the link to the next node in the list, respectively. The Node class has an initializer method that takes a value and an optional next node as arguments, and sets the value and next attributes accordingly.

The LinkedList class has two attributes: head, which stores a reference to the first node in the list, and tail, which stores a reference to the last node in the list. It also has an initializer method that sets head and tail to nil.

The LinkedList class has several methods that allow you to manipulate the list:

append(value): This method adds a new node with the given value to the end of the list. If the list is empty, the new node becomes both the head and the tail of the list. If the list is not empty, the new node becomes the new tail, and the link of the old tail node is updated to point to the new node.

pop(): This method removes the last element from the list and returns its value. If the list is empty, it returns nil. If the list has only one element, both the head and the tail are set to nil. If the list has more than one element, the link of the second-to-last node is updated to point to nil, and the tail is set to the second-to-last node.

find(value): This method searches for a node with the given value in the list, and returns its index. If the value is not found, it returns nil.

insert(value, index): This method inserts a new node with the given value at the specified index in the list. If the index is 0, the new node becomes the new head of the list. If the index is equal to the length of the list, the new node becomes the new tail. If the index is between 0 and the length of the list, the new node is inserted between two existing nodes.

## Hash table

```Ruby
class HashTable
  # The hash table has a fixed size and an array to store the key-value pairs
  attr_reader :size, :array

  def initialize(size)
    @size = size
    @array = Array.new(size)
  end

  # Hash a key to an index in the array
  def hash(key)
    key.hash % size
  end

  # Add a key-value pair to the hash table
  def insert(key, value)
    index = hash(key)
    if array[index].nil?
      array[index] = LinkedList.new
    end
    array[index].append({ key: key, value: value })
  end

  # Find the value for a given key
  def find(key)
    index = hash(key)
    list = array[index]
    return nil if list.nil?
    current_node = list.head
    while current_node
      return current_node.value[:value] if current_node.value[:key] == key
      current_node = current_node.next
    end
    nil
  end

  # Remove a key-value pair from the hash table
  def remove(key)
    index = hash(key)
    list = array[index]
    return nil if list.nil?
    current_node = list.head
    previous_node = nil
    while current_node
      if current_node.value[:key] == key
        if previous_node.nil?
          list.head = current_node.next
        else
          previous_node.next = current_node.next
        end
        return current_node.value[:value]
      end
      previous_node = current_node
      current_node = current_node.next
    end
    nil
  end
end
```

The HashTable class has two attributes: size, which is the fixed size of the hash table, and array, which is an array that stores the key-value pairs.

The initialize method takes a size as an argument and sets the size and array attributes. The array attribute is initialized as an array of the given size, with all elements set to nil.

The hash method takes a key as an argument and returns the index in the array where the key-value pair should be stored. It does this by applying the built-in hash method to the key and taking the modulus of the result with the size of the array.

The insert method takes a key and a value as arguments, and adds a key-value pair to the hash table. It does this by calling the hash method to get the index in the array, and then adding the key-value pair to a linked list at that index. If the array element at the index is nil, the method creates a new linked list and stores it at the index.

The find method takes a key as an argument and returns the value for that key. It does this by calling the hash method to get the index in the array, and then searching the linked list at that index for the key-value pair. If the key is found, it returns the value; if the key is not found, it returns nil.

## Rotating an array by K positions

```Ruby
# Rotate the array to the left
arr.each_with_index do |element, index|
  rotated_index = (index - k + arr.length) % arr.length
  rotated_arr[rotated_index] = element
end
```

This code snippet is rotating an array "arr" to the left by "k" number of positions. It does this by looping through each element in the array using the "each_with_index" method, and then calculates a new index position for each element based on its current index minus "k" and the length of the array. This new index is then used to place the element in a new array called "rotated_arr". The final step is to use the modulus operator to ensure that the new index stays within the bounds of the array.
