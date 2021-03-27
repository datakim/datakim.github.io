#!/use/bin/env python3
# -*- coding: utf-8 -*-
import time
# 모든 가설 투영을 이진법으로 바꾼다
hypo_old = [0xff, 0xf9, 0xfa, 0xfc, 0xcf, 0xd7, 0xe7, 0x7f,
            0xbf, 0xc9, 0xca, 0xcc, 0xd1, 0xd2, 0xd4, 0xe1,
            0xe2, 0xe4, 0x79, 0x7a, 0x7c, 0xb9, 0xba, 0xbc,
            0x4f, 0x57, 0x67, 0x8f, 0x97, 0xa7, 0x49, 0x4a,
            0x4c, 0x51, 0x52, 0x54, 0x61, 0x62, 0x64, 0x89,
            0x8a, 0x8c, 0x91, 0x92, 0x94, 0xa1, 0xa2, 0xa4]

# '와일드 카드'가 없는 경우
hypo_leaf = [0x49, 0x4a,
             0x4c, 0x51, 0x52, 0x54, 0x61, 0x62, 0x64, 0x89,
             0x8a, 0x8c, 0x91, 0x92, 0x94, 0xa1, 0xa2, 0xa4]


hypo_const = []
for i in range(48):
    hypo_const.append(0)
# print(hypo_const)
# print(len(hypo_const))

# 총 18개의 '와일드 카드;가 없는 가설이 존재
new_leaf = [0x20000, 0x10000,
            0x08000, 0x04000, 0x02000, 0x01000,
            0x00800, 0x00400, 0x00200, 0x00100,
            0x00080, 0x00040, 0x00020, 0x00010,
            0x00008, 0x00004, 0x00002, 0x00001]
n_count = 0
n_n = 48


def count(n_n: int, n_k: int, hypo_appear: list):
    global n_count
    pos_list = []
    hypo_process = []
    for i in range(n_k):
        pos_list.append(-1)
        hypo_process.append(0)
        # print(i)
        pass
    pos_index = 0
    while pos_list[0] <= n_n - n_k:
        if pos_index == 0:
            pos_list[pos_index] += 1
            if pos_list[pos_index] > n_n - n_k:
                break
                pass            
            hypo_process[pos_index] = hypo_const[pos_list[pos_index]]

            if hypo_process[pos_index] == 0x3ffff and pos_index < n_k - 1:
                continue
                pass
            else:
                pos_index += 1
                trend = 1  
                pass
            pass
        else:
            if trend == 1:               
                pos_list[pos_index] = pos_list[pos_index - 1] + 1
                pass           
            else:            
                pos_list[pos_index] += 1
                pass        
            if pos_list[pos_index] > n_n - n_k + pos_index:
                pos_index -= 1
                trend = 0
                continue
                pass            
            hypo_process[pos_index] = hypo_process[pos_index - 1] | hypo_const[pos_list[pos_index]]          
            if hypo_process[pos_index] == hypo_process[pos_index - 1] or \
                    (hypo_process[pos_index] == 0x3ffff and pos_index < n_k - 1):
                trend = 0
                continue
                pass
            pos_index += 1
            trend = 1
            pass      
        if pos_index == n_k:
            pos_index -= 1
            trend = 0
            if hypo_appear[hypo_process[pos_index]] == 0:
                hypo_appear[hypo_process[pos_index]] = 1
                n_count += 1
                pass
            pass
        pass
    return


if __name__ == '__main__':
   
    for i in range(48):
        for j in range(18):
            if hypo_old[i] | hypo_leaf[j] == hypo_old[i]:
                hypo_const[i] = hypo_const[i] | new_leaf[j]

    print('hypo_const : ')
    for x in hypo_const:
        print(x)
    change = 0
    hypo_appear = []
    for i in range(262144):
        hypo_appear.append(0)

    start_time = time.time()
    for i in range(1, 19):
       
        count(48, i, hypo_appear)
        print('length %-2d : %-10d' % (i, n_count))
        pass
    end_time = time.time()
    print('처리시간：')
    print(end_time - start_time, ' ', 's')
    pass

# Source：https://blog.csdn.net/qq_36614721/article/details/106404207
