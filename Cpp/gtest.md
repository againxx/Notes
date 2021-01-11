# Google Test

## How to write test suit

## Assertions
There are two kinds of assertion in gtest
* `ASSERT_*` which will raise fatal failure when assertions are not met and abort the execution
* `EXPECT_*` on the contrary will raise non-fatal failure and continue the execution (there is no expect assertion in pytset)

### Arithmetic assertions
* Equal: `EXPECT_EQ()` / `ASSERT_EQ` 

### String assertions
* Equal: `EXPECT_STREQ()` / `ASSERT_STREQ()`
* Not equal: `EXPECT_STRNE()` / `ASSERT_STRNE()`
