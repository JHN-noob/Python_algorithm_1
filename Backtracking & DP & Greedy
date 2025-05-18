백트래킹(Backtracking)

# 기본 원리
DFS 탐색 기반
선택 → 다음 단계로 넘어감(재귀 호출)
조건 불만족 → 가지치기(return)
다른 선택지로 넘어감 → 모든 경우의 수를 완전 탐색(트리 구조)

# 응용 문제
조합, 순열
부분집합
N-Queens
Sudoku
부분합 문제

# 기본 코드
def backtrack(상태):
    if 조건 만족:
        정답 저장 or 출력
        return
    for 선택지 in 가능한 선택지들:
        선택
        backtrack(재귀 호출, 다음 상태)
        선택 취소(원상복귀)

# 부분집합 예시 코드
def subsets(nums):
    result = []

    def dfs(index, path):
        result.append(path[:])
        for i in range(index, len(nums)):
            path.append(nums[i])
            dfs(i + 1, path)
            path.pop()

    dfs(0, [])
    return result

# 가지치기(Pruning)
부분합 문제에서 타겟보다 합한 숫자가 크면
if current_sum > target:
    return

# 그렇다면 for문이 필요하냐?
아니다. 존재 여부만 찾는 True or False 방식이 있고
모든 경우의 수를 찾는 return 방식(모든 노드를 다 훑음)이 있지만
선택지가 인덱스를 더함, 인덱스를 더하지 않음만 있기에 for문이 필요없다.

# 부분합 문제 실전 코드
def solution(d, budget):
    result = []

    def dfs(index, curr_sum, count):
        if curr_sum == budget: # 합한 숫자와 버짓이 같으면 count를 저장하고 탈출
            result.append(count)
            return

        if index == len(d) or curr_sum > budget: # 인덱스가 배열 크기와 같거나 합한 숫자가 버짓보다 크면 탈출
            return

        dfs(index+1, curr_sum+d[index], count+1) # 선택함
        dfs(index+1, curr_sum, count) # 선택안함

    dfs(0, 0, 0) # 초기값
    return max(result) if result else 0 # result에 결과가 없을 경우 0 출력

이렇게 했으나 d의 원소가 최대 100개라서 효율성이 떨어진다..


DP (Dynaminc Programming)

# 바텀업 DP(부분합 문제)
def solution(d, budget):
    result = [[] for _ in range(budget+1)] # budget당 조합의 길이를 구하기 위해 이중 배열
    result[0] = [0] # 아무것도 안고른 값은 0
    
    for i in d:
        for j in range(budget, i-1, -1): # 각 원소를 1개씩만 쓰기 위해 내림차순으로 돌림
            for length in result[j-i]: # result[j-i]에 값이 있다면 result[j] += 1
                result[j].append(length+1)

    return max(result[budget]) if result[budget] else 0

# 바텀업 DP(부분합 문제 최적화 버전)
def solution(d, budget):
    result = [-1] * (budget+1) # budget에 해당하는 값을 누적
    result[0] = 0 # 아무것도 안고른 값은 0
    
    for i in d:
        for j in range(budget, i-1, -1): # 각 원소를 1개씩만 쓰기 위해 내림차순으로 돌림
            if result[j-i] != -1: # result[j-i]이 -1이 아니라면
                result[j] = max(result[j], result[j-i]+1) # result[j]와 result[j-i] 중 큰 값을 저장

    return result[budget] if result[budget] != -1 else 0

# 바텀업 DP(부분합 문제, budget 이하도 포함)
def solution(d, budget):
    dp = [0] * (budget+1)
    
    for i in d:
        for j in range(budget, i-1, -1):
            dp[j] = max(dp[j], dp[j-i]+1)
    
    return max(dp)

# 탑다운 DP(백트래킹 + 메모이제이션)
def solution(d, budget):
    n = len(d)
    memo = {}
    
    def dfs(index, remaining):
        if remaining == 0:
            return 0
        if index == n or remaining < 0:
            return -1
        
        key = (index, remaining)
        if key in memo:
            return memo[key]
        
        use = dfs(index+1, remaining-d[index])
        if use != -1:
            use += 1
        
        skip = dfs(index+1, remaining)
        
        memo[key] = max(use, skip)
        return memo[key]
    
    result = dfs(0, budget)
    
    return result if result != -1 else 0

바텀업과 탑다운 DP 모두 budget이 커질 때(10,000,000) 속도가 너무 느렸고 budget과 꼭 일치하는 조합을 찾아야되는 것으로 오해했다...


그리디(Greedy)

# 오름차순 정렬 + budget 미만 합일 때의 카운트를 출력
def solution(d, budget):
    d.sort()
    total, count = 0, 0
    for i in d:
        if total + i <= budget:
            total += i
            count += 1
        else:
            break
            
    return count

문제해결..
