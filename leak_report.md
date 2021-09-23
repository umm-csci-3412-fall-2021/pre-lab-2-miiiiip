# Leak report
In line 41 of check_whitespace.c there is memory allocated for the resulting array of "strip".
This memory was not being freed after it's use, therefore resulting in a memory leak.
However, because the result of this function is the memory being saved,
the function "strip" itself isn't able to free the memory.
This means that after the use of strip in "is_clean", we must free the string "cleaned"
which is the resulting memory created by strip.
This is okay, because the result of "is_clean" is a number between 0 and 1,
and there is no reason to keep the memory that "strip" created allocated anymore.
