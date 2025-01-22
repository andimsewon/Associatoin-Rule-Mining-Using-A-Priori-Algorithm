import csv
import math
import sys
from collections import Counter

# 데이터 저장 구조
class Data:
    def __init__(self, features, label):
        self.features = features
        self.label = label

# 노드 구조체 정의
class Node:
    def __init__(self, feature=None, label=None):
        self.feature = feature
        self.label = label
        self.children = {} #분할된 자식 노드 저장하는 딕셔너리

# CSV 파일 읽기 함수
def read_csv(filename):
    with open(filename, 'r') as file:
        reader = csv.reader(file)
        headers = next(reader)
        dataset = []
        for row in reader:
            features = {headers[i]: row[i] for i in range(len(headers) - 1)}
            label = row[-1]
            dataset.append(Data(features, label))
    return dataset, headers[:-1]

# 엔트로피 계산 함수
def calculate_entropy(dataset):
    label_count = Counter([data.label for data in dataset])
    total = len(dataset)
    entropy = 0.0
    for count in label_count.values():
        p = count / total
        entropy -= p * math.log2(p)
    return entropy

# 정보 이득 계산 함수
def calculate_information_gain(dataset, feature):
    total_entropy = calculate_entropy(dataset)
    feature_values = set(data.features[feature] for data in dataset)
    subset_entropy = 0.0

    for value in feature_values:
        subset = [data for data in dataset if data.features[feature] == value]
        p = len(subset) / len(dataset)
        subset_entropy += p * calculate_entropy(subset)
    return total_entropy - subset_entropy

# 결정 트리 생성 함수
def build_decision_tree(dataset, features):
    labels = [data.label for data in dataset]
    # 모든 데이터가 같은 레이블을 가지는 경우 리프 노드 생성
    if len(set(labels)) == 1:
        return Node(label=labels[0])

    # 사용할 특징이 더 이상 없는 경우, 가장 빈도가 높은 레이블 선택
    if not features:
        most_common_label = Counter(labels).most_common(1)[0][0]
        return Node(label=most_common_label)

    # 정보 이득이 가장 큰 특징 선택
    best_feature = max(features, key=lambda f: calculate_information_gain(dataset, f))
    node = Node(feature=best_feature)

    # 선택된 특징으로 데이터 분할
    feature_values = set(data.features[best_feature] for data in dataset)
    remaining_features = [f for f in features if f != best_feature]

    for value in feature_values:
        subset = [data for data in dataset if data.features[best_feature] == value]
        child_node = build_decision_tree(subset, remaining_features)
        node.children[value] = child_node

    return node

# 트리를 if-then 형식으로 출력하는 함수
def print_tree(node, prefix=""):
    if node.label is not None:
        print(f"{prefix}THEN {node.label}")
        return

    for value, child in node.children.items():
        print(f"{prefix}IF {node.feature} == {value}", end=" ")
        print_tree(child, prefix + "AND ")

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python 202312123_ML_hw1.py playtennis.csv")
        sys.exit(1)

    filename = sys.argv[1]
    dataset, features = read_csv(filename)
    tree = build_decision_tree(dataset, features)
    print_tree(tree)

