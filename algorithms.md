# What is an algorithm

In the most general sense, an algorithm is a series of instructions telling a computer how to transform a set of facts about the world into useful information. The facts are data, and the useful information is knowledge for people, instructions for machines or input for yet another algorithm. There are many common examples of algorithms, from sorting sets of numbers to finding routes through maps to displaying information on a screen

We can have a daily life example to understand more, Think about eating spaghetti meal for lunch, How would you down you're process . Answering the question is a detailed way yields an algorithm, Also if you ask one of you're friends might give you different way to have a spaghetti meal. You might have more than algorithm for the same output. Each algorithm has its own pros and cons you will need to think carefully and take care of time, cost, etc when picking an algorithm to get any output
# Binary Search

Binary search only works when your list is in sorted order. For example, the names in a phone book are sorted in alphabetical order, so you can use binary search to look for a name.

The binary_search function takes a sorted array and an item. If the item is in the array, the function returns its position. You’ll keep track of what part of the array you have to search through. At the beginning, this is the entire array

```ruby
def binary_search(list, item)
  low = 0
  high = list.length - 1

  while low <= high
    mid = (low + high)
    guess = list[mid]
    if guess == item
      return mid
    elsif guess > item
      high = mid - 1
    else
      low = mid + 1
    end
  end
end

my_list = [1, 3, 5, 7, 9]
p binary_search(my_list, 3) # 1
p binary_search(my_list, 66) # nil
```

# Big O notation

Big O notation is special notation that tells you how fast an algorithm is. Who cares? Well, it turns out that you’ll use other people’s algorithms often—and when you do, it’s nice to understand how fast or slow they are

Big O notation tells you how fast an algorithm is. For example, suppose you have a list of size n. Simple search needs to check each element, so it will take n operations. The run time in Big O notation is O(n). Where are the seconds? There are none—Big O doesn’t tell you the speed in seconds. Big O notation lets you compare the number of operations. It tells you how fast the algorithm grows.

## Some common Big O run times

Here are five Big O run times that you’ll encounter a lot, sorted from fastest to slowest:

- O(log n), also known as log time. Example: Binary search
- O(n), also known as linear time. Example: Simple search
- O(n \* log n). Example: A fast sorting algorithm, like quicksort (coming up in chapter 4)
- O(n2). Example: A slow sorting algorithm, like selection sort (coming up in chapter 2)
- O(n!). Example: A really slow algorithm, like the traveling salesperson (coming up next!)

### Recap
• Binary search is a lot faster than simple search.
• O(log n) is faster than O(n), but it gets a lot faster once the list of items you’re searching through grows.
• Algorithm speed isn’t measured in seconds.
• Algorithm times are measured in terms of growth of an algorithm.
• Algorithm times are written in Big O notation.

