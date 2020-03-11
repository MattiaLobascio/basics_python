{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "slide"
    }
   },
   "source": [
    "\n",
    " # Important Python Programming Aspects\n",
    "\n",
    "- Mutable/Imutable Objects\n",
    "- Multiprocessing\n",
    "- List Comprehension\n",
    "- Sorting, Min and Max operators   "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "slide"
    }
   },
   "source": [
    "## Mutable and Imutable Objects\n",
    "\n",
    "- Immutable Objects\n",
    "    - Strings\n",
    "    - Tuples\n",
    "- Mutable Objectes\n",
    "    - Lists\n",
    "    - Dictionaries"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "###  A mutable object (such as list) can change without altering the reference "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {
    "slideshow": {
     "slide_type": "-"
    }
   },
   "outputs": [],
   "source": [
    "a = [1, 2, 3] \n",
    "a[1] = 3"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "-"
    }
   },
   "source": [
    "What is the value of a?"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[1, 3, 3]"
      ]
     },
     "execution_count": 2,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "a"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "### An immutable object (such as tupple or a string) cannot!"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "3\n"
     ]
    }
   ],
   "source": [
    "a = (1, 2, 3)\n",
    "print(a[2])\n",
    "# a[1] = 3"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "l\n"
     ]
    }
   ],
   "source": [
    "a = \"Hello\"\n",
    "print(a[2])\n",
    "# a[1] = 3"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "### Multiple references can point to the same object"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {
    "slideshow": {
     "slide_type": "-"
    }
   },
   "outputs": [],
   "source": [
    "a = [1, 2, 3]\n",
    "b = a\n",
    "a[1] = 3"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "source": [
    "What is the value of b?"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[1, 3, 3]"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "b  "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Memory address of a: 0x7fe8dcc1fa48\n",
      "Memory address of b: 0x7fe8dcc1fa48\n"
     ]
    }
   ],
   "source": [
    "a = [1, 2, 3]\n",
    "b = a\n",
    "a[1] = 3\n",
    "\n",
    "address_a = hex(id(a))\n",
    "address_b = hex(id(b))\n",
    "\n",
    "print(f\"Memory address of a: {address_a}\")\n",
    "print(f\"Memory address of b: {address_b}\")\n",
    "\n",
    "assert address_a == address_b"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "Example on why mutability is important"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "outputs": [],
   "source": [
    "def is_same_reversed_list(input_list: list) -> bool:\n",
    "    \"\"\" \n",
    "    Returns True if the input list is equal to it' s reverse, else return False \n",
    "    \n",
    "    Example:\n",
    "    >>> input_list = [4, 3, 4]\n",
    "    >>> is_same_reversed_list(input_list) # This is True\n",
    "    \"\"\"\n",
    "    \n",
    "    # Create copy of input list\n",
    "    copy_input_list = input_list\n",
    "    \n",
    "    # Reverse copy of input list\n",
    "    copy_input_list.reverse()  # Inplace operation\n",
    "\n",
    "    return copy_input_list == input_list"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [],
   "source": [
    "input_list1 = [1, 2, 1]\n",
    "input_list2 = [1, 2, 3]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Result for input_list1: True\n"
     ]
    }
   ],
   "source": [
    "print(f\"Result for input_list1: {is_same_reversed_list(input_list1)}\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Result for input_list2: True\n"
     ]
    }
   ],
   "source": [
    "print(f\"Result for input_list2: {is_same_reversed_list(input_list2)}\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "outputs": [],
   "source": [
    "def is_same_reversed_list_fixed(input_list: list) -> bool:\n",
    "    \"\"\" \n",
    "    Returns True if the input list is equal to it' s reverse, else return False \n",
    "    \n",
    "    Example:\n",
    "    >>> input_list = [4, 3, 4]\n",
    "    >>> is_same_reversed_list(input_list) # This is True\n",
    "    \"\"\"\n",
    "    \n",
    "    # Create copy of input list\n",
    "    copy_input_list = input_list.copy()\n",
    "    \n",
    "    # Reverse copy of input list\n",
    "    copy_input_list.reverse() # Inplace operation\n",
    "\n",
    "    return copy_input_list == input_list"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Result for input_list1: True\n",
      "Result for input_list2: False\n"
     ]
    }
   ],
   "source": [
    "input_list1 = [1, 2, 1]\n",
    "input_list2 = [1, 2, 3]\n",
    "print(f\"Result for input_list1: {is_same_reversed_list_fixed(input_list1)}\")\n",
    "print(f\"Result for input_list2: {is_same_reversed_list_fixed(input_list2)}\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "Rewriting that function in the Pythonic way"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {
    "slideshow": {
     "slide_type": "-"
    }
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "True"
      ]
     },
     "execution_count": 14,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "input_list = [1, 2, 2, 1]\n",
    "input_list == input_list[::-1]"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "One more list copy example"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[[1, 2, 3], [2, 99, 5], [5, 6, 7]]"
      ]
     },
     "execution_count": 15,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "a = [[1, 2, 3],\n",
    "     [2, 4, 5],\n",
    "     [5, 6, 7]]\n",
    "\n",
    "b = a.copy()\n",
    "a[1][1] = 99\n",
    "a"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "What is the result of b"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[[1, 2, 3], [2, 99, 5], [5, 6, 7]]"
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "b"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "Shallow Copy vs Deep Copy\n",
    "- Shallow copy will not copy child objects\n",
    "- Deep copy clones everything recursively"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[[1, 2, 3], [2, 99, 5], [5, 6, 7]]"
      ]
     },
     "execution_count": 17,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "from copy import deepcopy\n",
    "\n",
    "a = [[1, 2, 3],\n",
    "     [2, 4, 5],\n",
    "     [5, 6, 7]]\n",
    "\n",
    "b = deepcopy(a)\n",
    "a[1][1] = 99\n",
    "a"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[[1, 2, 3], [2, 4, 5], [5, 6, 7]]"
      ]
     },
     "execution_count": 18,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "b"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "### Summary\n",
    "- Try to use immutable objects when you are sure you do not need to change the object (tuple instead of lists)\n",
    "- If you need to copy, make sure you use the right type of copying mechanism (Shallow vs Deep)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "slide"
    }
   },
   "source": [
    "## Multiprocessing (Not multithreading)\n",
    "- Concurrently run a program on different cores of a CPU, using a different memory space\n",
    "- Speed up CPU bound problems\n",
    "- [Python Multiprocessing library](https://docs.python.org/3.8/library/multiprocessing.html)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "### Measuring elapsed time on Python\n",
    "- [Timeit Module](https://docs.python.org/3.8/library/timeit.html)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Elapsed time 0.1272750999996788s\n"
     ]
    }
   ],
   "source": [
    "from timeit import default_timer as timer\n",
    "st = timer() # Starting time\n",
    "\n",
    "# Do something\n",
    "a = []\n",
    "for i in range(1000000):\n",
    "    a.append(i)\n",
    "\n",
    "et = timer() # Ending time\n",
    "elapsed_time = et-st\n",
    "print(f\"Elapsed time {elapsed_time}s\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "### Map operation and anonymous functions\n",
    "- Map is a higher-order function (takes another function as argument) that applies a given function to each element of a iterable (Eg. List)\n",
    "- Anonymous or lambda functions are functions that are defined without a name"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "Task: Create a of strings, based on another list, with \"Odd\" where the element of the first list is odd and \"Even\" otherwise\n",
    "\n",
    "Example:\n",
    "```python\n",
    "    fist_list = [3, 5, 2, 9]\n",
    "    result = ['Odd', 'Odd', 'Even', 'Odd']\n",
    "```"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "['Odd', 'Odd', 'Even', 'Odd']"
      ]
     },
     "execution_count": 20,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "first_list = [3, 5, 2, 9]\n",
    "\n",
    "# The python way with list compreention (More on this later)\n",
    "[\"Even\" if x%2==0 else \"Odd\" for x in first_list]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "['Odd', 'Odd', 'Even', 'Odd']"
      ]
     },
     "execution_count": 21,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Using map (Usefull for multiprocessing)\n",
    "# Syntax of map: map(function, iterable)\n",
    "\n",
    "list(\n",
    "    map(lambda x: \"Even\" if x%2==0 else \"Odd\", first_list)\n",
    ")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "#### Example with some text processing"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "metadata": {
    "slideshow": {
     "slide_type": "-"
    }
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "['hello', 'my', 'name', 'is', 'david']"
      ]
     },
     "execution_count": 22,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "from time import sleep  # Just used to simulate other operations\n",
    "\n",
    "text_string = \"Hello my name is , David, . \"\n",
    "\n",
    "def clean_text(text_string: str) -> list:\n",
    "    \"\"\" Lower the case of every string and removes empty spaces and punctuation \"\"\"\n",
    "    \n",
    "    # Split text into list \n",
    "    text_list = text_string.split()\n",
    "    processed_list = list()\n",
    "    \n",
    "    for word in text_list:\n",
    "        processed_word = word.lower().strip(\".,\")\n",
    "        if processed_word != \"\":\n",
    "            processed_list.append(processed_word)\n",
    "        \n",
    "    # Do some other operations\n",
    "    sleep(3)  # Sleep for 3 seconds\n",
    "    \n",
    "    return processed_list\n",
    "\n",
    "clean_text(text_string)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "Pro tip: You can use \"%%time\" to measure elapsed time on a cell on notebooks"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Size of text_list: 50\n",
      "CPU times: user 1.07 ms, sys: 130 µs, total: 1.2 ms\n",
      "Wall time: 884 µs\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "'Hello my name is , David, . Hello my name is , David, . Hello my name is , David, . Hello my name is , David, . Hello my name is , David, . Hello my name is , David, . Hello my name is , David, . Hello my name is , David, . Hello my name is , David, . Hello my name is , David, . '"
      ]
     },
     "execution_count": 23,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%%time\n",
    "\n",
    "# Generating a random text list\n",
    "size_list = 50\n",
    "text_to_process = [text_string*10 for _ in range(size_list)]\n",
    "\n",
    "print(f\"Size of text_list: {len(text_to_process)}\")\n",
    "text_to_process[0]"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "#### Single Process"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "CPU times: user 11.3 ms, sys: 11.7 ms, total: 23 ms\n",
      "Wall time: 2min 30s\n"
     ]
    }
   ],
   "source": [
    "%%time\n",
    "result = list(map(clean_text, text_to_process))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "#### Multi Process"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "My computer has 4 cores\n",
      "CPU times: user 106 ms, sys: 50.7 ms, total: 157 ms\n",
      "Wall time: 1min\n"
     ]
    }
   ],
   "source": [
    "%%time\n",
    "\n",
    "import multiprocessing as mp\n",
    "\n",
    "n_cpu = mp.cpu_count() \n",
    "print(f\"My computer has {n_cpu} cores\")\n",
    "\n",
    "pool = mp.Pool(n_cpu-1) # Always use the total count of cores - 1\n",
    "result = list(pool.map(clean_text, text_to_process))\n",
    "\n",
    "# Close the pool object\n",
    "pool.close()\n",
    "pool.join()   "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "### Creating Processes Overhead"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [],
   "source": [
    "def odd_or_even(x: int) -> str:\n",
    "    \"\"\" Returns  ODD if number is odd else return EVEN \"\"\"\n",
    "    if x % 2 == 0:\n",
    "        return \"EVEN\"\n",
    "    else: \n",
    "        return \"ODD\""
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "CPU times: user 161 µs, sys: 27 µs, total: 188 µs\n",
      "Wall time: 193 µs\n"
     ]
    }
   ],
   "source": [
    "%%time\n",
    "first_list = list(range(1000))\n",
    "result = list(map(odd_or_even, first_list))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "CPU times: user 5.52 ms, sys: 13 ms, total: 18.6 ms\n",
      "Wall time: 123 ms\n"
     ]
    }
   ],
   "source": [
    "%%time\n",
    "\n",
    "pool = mp.Pool(n_cpu-1) # Always use the total count of cores - 1\n",
    "result = list(pool.map(odd_or_even, first_list))\n",
    "\n",
    "# Close the pool object\n",
    "pool.close()\n",
    "pool.join()  "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "### Summary Multiprocessing\n",
    "- Check [Python Multiprocessing library](https://docs.python.org/3.8/library/multiprocessing.html) page\n",
    "- Be carefull with overhead when using multiprocess, because your code can become slower, instead of faster"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "slide"
    }
   },
   "source": [
    "## List Comprehension \n",
    "- Very important and very common Python pattern\n",
    "- MUCH more efficient than for loops"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "Task: Create a new list with the numbers in the input list multiplied by 2\n",
    "\n",
    "Example:\n",
    "```python\n",
    "    input_list = [1, 2, 3, 4, 5, 6, 7, 8, 9]\n",
    "    result = [2, 4, 6, 8, 10, 12, 14, 16, 18]\n",
    "```"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[2, 4, 6, 8, 10, 12, 14, 16, 18]"
      ]
     },
     "execution_count": 29,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "input_list = [1, 2, 3, 4, 5, 6, 7, 8, 9]\n",
    "[x*2 for x in input_list]"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "Task: Create a new list with only even numbers from the input list\n",
    "\n",
    "Example:\n",
    "```python\n",
    "    input_list = [1, 2, 3, 4, 5, 6, 7, 8, 9]\n",
    "    result = [2, 4, 6, 8]\n",
    "```"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 30,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[2, 4, 6, 8]"
      ]
     },
     "execution_count": 30,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "input_list = [1, 2, 3, 4, 5, 6, 7, 8, 9]\n",
    "[x for x in input_list if x%2 == 0]"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "### Summary List Comprehension \n",
    " - Very fast and readable alternative to for loops\n",
    " - Can also be used to create dictionaries (Dict Comprehension)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "slide"
    }
   },
   "source": [
    "## Sorting, Min and Max"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 31,
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Sorted list ascending : [3, 3, 5, 6, 6, 7, 9, 20, 80]\n",
      "Sorted list descending: [80, 20, 9, 7, 6, 6, 5, 3, 3]\n"
     ]
    }
   ],
   "source": [
    "input_list = [5, 80, 3, 6, 20, 6, 7, 3, 9]\n",
    "\n",
    "print(f\"Sorted list ascending : {sorted(input_list)}\")\n",
    "print(f\"Sorted list descending: {sorted(input_list, reverse=True)}\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "### Example with sorting strings"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 32,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "['I', 'know', 'how', 'to', 'program', 'the', 'Python', 'language']"
      ]
     },
     "execution_count": 32,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "input_list = \"I know how to program the Python language\".split()\n",
    "input_list"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "Task: Sort a list of strings by the third character, if the string is longer than three characters\n",
    "\n",
    "Example:\n",
    "```python\n",
    "    input_list = ['I', 'know', 'how', 'to', 'program', 'the', 'Python', 'language']\n",
    "    result = ['the', 'language', 'know', 'program', 'Python', 'how']\n",
    "```"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "['the', 'language', 'know', 'program', 'Python', 'how']"
      ]
     },
     "execution_count": 33,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "sorted([s for s in input_list if len(s) >= 3], key=lambda x: x[2])"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "Task: Get the row of a list of lists with the lowest sum\n",
    "Example:\n",
    "```python\n",
    "    input_list = [[-1, -5, 3, 56], \n",
    "                  [5, 3, 7, 6, 1],\n",
    "                  [7, 4, -10, 123],\n",
    "                  [6, 3, 8, 3]]\n",
    "    \n",
    "    result = [6, 3, 8, 3]\n",
    "```"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "metadata": {
    "slideshow": {
     "slide_type": "fragment"
    }
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[6, 3, 8, 3]"
      ]
     },
     "execution_count": 34,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "input_list = [[-1, -5, 3, 56], \n",
    "              [5, 3, 7, 6, 1],\n",
    "              [7, 4, -10, 123],\n",
    "              [6, 3, 8, 3]]\n",
    "\n",
    "min(input_list, key=lambda x: sum(x))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "slideshow": {
     "slide_type": "subslide"
    }
   },
   "source": [
    "### Summary Sorting, Min and Max operators\n",
    "- Using the key parameter you can specify a function that will return the value through which the inputs will be sorted"
   ]
  }
 ],
 "metadata": {
  "celltoolbar": "Slideshow",
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.6.9"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}
