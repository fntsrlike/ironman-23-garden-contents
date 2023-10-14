---
title: Wiki Link 渲染示例
created_at: 2023-10-07T23:22:42.800+08:00
published_at: 2023-10-07T23:22:56.834+08:00
tags: []
---
## Text Link Testing:

### Regular Case

```
- Expected:
    - single `[]`: [/dev/testcases/note]
    - double `[]`: [note](/dev/testcases/note)
    - double `[]` with alias: [My Note](/dev/testcases/note)
- Actual:
    - single `[]`: [/dev/testcases/note]
    - double `[]`: [[/dev/testcases/note]]
    - double `[]` with alias: [[/dev/testcases/note|My Note]]
```

- Expected:
    - single `[]`: [/dev/testcases/note]
    - double `[]`: [note](/dev/testcases/note)
    - double `[]` with alias: [My Note](/dev/testcases/note)
- Actual:
    - single `[]`: [/dev/testcases/note]
    - double `[]`: [[/dev/testcases/note]]
    - double `[]` with alias: [[/dev/testcases/note|My Note]]

### Special Case Testing

#### Number

```
- Expected: 
    - [100](</dev/testcases/100>)
- Actually: 
    - [[/dev/testcases/100|100]]
```

- Expected: 
    - [100](</dev/testcases/100>)
- Actually: 
    - [[/dev/testcases/100|100]]
 

#### Han

```
- Expected: 
    - [測試](</dev/testcases/%E6%B8%AC%E8%A9%A6>)
    - [測試](</dev/testcases/測試>)
- Actually: 
    - [[/dev/testcases/%E6%B8%AC%E8%A9%A6|測試]]
    - [[/dev/testcases/測試|測試]]
```

- Expected: 
    - [測試](</dev/testcases/%E6%B8%AC%E8%A9%A6>)
    - [測試](</dev/testcases/測試>)
- Actually: 
    - [[/dev/testcases/%E6%B8%AC%E8%A9%A6|測試]]
    - [[/dev/testcases/測試|測試]]


#### Symbol

```
- Expected:
    - dot: [test.with.space](</dev/testcases/test.with.space>)
    - dash: [test-with-space](</dev/testcases/test-with-space>)
    - underscore: [test_with_space](</dev/testcases/test_with_space>)
- Actually:
    - dot: [[/dev/testcases/test.with.space|test.with.space]]
    - dash: [[/dev/testcases/test-with-space|test-with-space]]
    - underscore: [[/dev/testcases/test_with_space|test_with_space]]
```

- Expected:
    - dot: [test.with.space](</dev/testcases/test.with.space>)
    - dash: [test-with-space](</dev/testcases/test-with-space>)
    - underscore: [test_with_space](</dev/testcases/test_with_space>)
- Actually:
    - dot: [[/dev/testcases/test.with.space|test.with.space]]
    - dash: [[/dev/testcases/test-with-space|test-with-space]]
    - underscore: [[/dev/testcases/test_with_space|test_with_space]]

#### Space with URL encoding
```
- Expected:
    - Space: [test with space](</dev/testcases/test%20with%20space>)
- Actually:
    - Space: [[/dev/testcases/test%20with%20space|test with space]]
```

- Expected:
    - Space: [test with space](</dev/testcases/test%20with%20space>)
- Actually:
    - Space: [[/dev/testcases/test%20with%20space|test with space]]

#### Url enclosed in angle brackets
```
- Expected: [angle](</dev/testcases/angle>)
- Actually: [[</dev/testcases/angle>|angle]]
```
 
- Expected: [angle](</dev/testcases/angle>)
- Actually: [[</dev/testcases/angle>|angle]]

#### Han
```
- Expected:
    - Space: [測試](</dev/testcases/測試>)
- Actually:
    - Space: [[/dev/testcases/測試|測試]]
```

- Expected:
    - Space: [測試](</dev/testcases/測試>)
- Actually:
    - Space: [[/dev/testcases/測試|測試]]

#### Mixed
```
- Expected:
    - [測-試_mix.ed 的.情%20況](</dev/testcases/測-試_mix.ed 的.情%20況>)
- Actually
    - [[/dev/testcases/測-試_mix.ed 的.情%20況|測-試_mix.ed 的.情%20況]]
```

- Expected:
    - [測-試_mix.ed 的.情%20況](</dev/testcases/測-試_mix.ed 的.情%20況>)
- Actually
    - [[/dev/testcases/測-試_mix.ed 的.情%20況|測-試_mix.ed 的.情%20況]]



