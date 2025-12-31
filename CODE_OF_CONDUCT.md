#include <iostream>
#include <vector>

using namespace std;

class PermutationGenerator {
private:
    vector<vector<int>> result;
    
    void backtrack(vector<int>& path, vector<int>& choices) {
        if (choices.empty()) {
            result.push_back(path);
            return;
        }
        
        for (int i = 0; i < choices.size(); i++) {
            int current = choices[i];
            path.push_back(current);
            
            vector<int> remaining;
            for (int j = 0; j < choices.size(); j++) {
                if (j != i) remaining.push_back(choices[j]);
            }
            
            backtrack(path, remaining);
            path.pop_back();
        }
    }
    
public:
    // 直接生成并存储在 result 中
    void generate(vector<int>& nums) {
        result.clear();
        vector<int> path;
        vector<int> choices = nums;
        backtrack(path, choices);
    }
    
    // 获取结果的方法
    vector<vector<int>>& getResult() {
        return result;
    }
};

int main() {
    PermutationGenerator generator;
    vector<int> nums = {1, 2, 3};
    
    // 直接生成，结果存储在 generator 内部
    generator.generate(nums);
    
    // 直接访问 result
    cout << "1,2,3的全排列：" << endl;
    int index = 1;
    for (auto& perm : generator.getResult()) {
        cout << index++ << ". ";
        for (int num : perm) {
            cout << num << " ";
        }
        cout << endl;
    }
    
    return 0;
}
