# Debugging Practices

## 1. Locate the Fault

When a test fails, the first step is to determine the origin of the error. Is the fault in the test itself (e.g., incorrect assertion, setup issues) or in the component code being tested? Careful analysis is required to pinpoint the source.

## 2. Fix Appropriately

Once the fault location is identified, apply the fix to the root cause:
*   If the test logic is flawed, correct the test.
*   If the component code is incorrect, fix the component.

## 3. Preserve Test Integrity

Crucially, when a failing test correctly identifies a bug in the component code, **do not modify the test with mocks, stubs, or fallback logic simply to make it pass.** The test's purpose is to verify the actual behavior of the component under test. Modifying the test to avoid fixing the component undermines the value of the test suite and masks underlying issues. Fix the component code to meet the test's expectations.