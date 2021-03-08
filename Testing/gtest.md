# Google Test

## How to write test suit

## Assertions
There are two kinds of assertion in gtest
* `ASSERT_*` which will raise **fatal** failure when assertions are not met and abort the current function (other functions will still be tested)
* `EXPECT_*` on the contrary will raise **non-fatal** failure and continue the execution (there is no expect assertion in pytset)
* To provide a custom failure message, stream it into the macro using the `<<` operator

### Basic assertions
* Condition true: `EXPECT_TRUE(condition) / ASSERT_TRUE(condition)`
* Condition false: `EXPECT_FALSE(condition) / ASSERT_FALSE(condition)`

### Binary assertions
* `val1 == val2`: `EXPECT_EQ(val1, val2)` / `ASSERT_EQ(val1, val2)`
* `val1 != val2`: `EXPECT_NE(val1, val2)` / `ASSERT_NE(val1, val2)`
* `val1 < val2`: `EXPECT_LT(val1, val2)` / `ASSERT_LT(val1, val2)`
* `val1 <= val2`: `EXPECT_LE(val1, val2)` / `ASSERT_LE(val1, val2)`
* `val1 > val2`: `EXPECT_GT(val1, val2)` / `ASSERT_GT(val1, val2)`
* `val1 >= val2`: `EXPECT_GE(val1, val2)` / `ASSERT_GE(val1, val2)`

### String assertions
* For pointer, `*_EQ` only compares the pointer value, so we need `*_STREQ` assertion for c-style strings
* Equal: `EXPECT_STREQ()` / `ASSERT_STREQ()` / `ASSERT_STREQ(c_string, NULL)`
    - for C++11 and above, use `*_EQ(c_string, nullptr)` for both c-style strings or other pointers
    - a `NULL` pointer and an empty string are considered *different*
* Not equal: `EXPECT_STRNE()` / `ASSERT_STRNE()`
* Ignoring case equal: `EXPECT_STRCASEEQ() / ASSERT_STRCASEEQ()`
* Ignoring case not equal: `EXPECT_STRCASENE() / ASSERT_STRCASENE()`
