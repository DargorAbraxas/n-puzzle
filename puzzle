# -*- coding: utf-8 -*-
"""
Created on Thu Mar 02 20:18:33 2017

@author: Dargor
"""
'n-puzzle game solver using breath first search and depth first search algorithms'

#Import libraries
import collections 
import math
import os
import sys
import time


#Declare tuple subtype for nodes
Node = collections.namedtuple('Node', 'state cost parent move depth')

#Print board
def board(state):
    #Check if input is valid
    if state == 0:
        print '0'
    else: 
        #Row size
        size = int(math.sqrt(len(state)))
        #Build list
        row = []
        for i in range(size):
            row.append(i*size)
        #Build board        
        for i in row:
            print state[i:i+size]

#Find goal state            
def goal(state):
    n = len(state)
    goal = []
    #Build goal
    for i in range(n):
        goal.append(i)
    return tuple(goal)

#Move tile up        
def up(state):
    state_l = list(state)
    #Size of square
    size = int(math.sqrt(len(state_l)))
    #Find 0
    index = state_l.index(0)
    #Check if not in top row
    if index not in range(size):
        #Move up
        state_l[index-size], state_l[index] = state_l[index],state_l[index-size]
        state = tuple(state_l)
        return state
    else:
        return 0

#Move tile down    
def down(state):
    state_l = list(state)
    #Size of square
    size = int(math.sqrt(len(state_l)))
    #Find 0
    index = state_l.index(0)
    #Check if not in last row
    if index not in range(size*(size-1),size*size):
        #Move down
        state_l[index+size], state_l[index] = state_l[index], state_l[index+size]
        state = tuple(state_l)
        return state
    else:
        return 0

#Move left    
def left(state):
    state_l = list(state)
    #Size of square
    size = int(math.sqrt(len(state_l)))
    #Find 0
    index = state_l.index(0)
    #Check not in left column
    if index not in range(0,len(state),size):
        #Move left
        state_l[index-1], state_l[index] = state_l[index], state_l[index-1]
        state = tuple(state_l)
        return state
    else:
        return 0

#Move right    
def right(state):
    state_l = list(state)
    #Size of square
    size = int(math.sqrt(len(state_l)))
    #Find 0
    index = state_l.index(0)
    #Check not in right column
    if index not in range(size-1,len(state_l),size):
        #Move right
        state_l[index+1], state_l[index] = state_l[index], state_l[index+1]
        state = tuple(state_l)
        return state
    else:
        return 0
    
#Expand nodes
def expand(parent):
    expanded = []
    expanded.append(Node(up(parent.state), parent.cost+1, parent, "Up", parent.depth + 1))
    expanded.append(Node(down(parent.state), parent.cost+1, parent,"Down", parent.depth + 1))
    expanded.append(Node(left(parent.state), parent.cost+1, parent, "Left", parent.depth + 1))
    expanded.append(Node(right(parent.state), parent.cost+1, parent, "Right", parent.depth + 1))
    
    #Ignore invalid states
    expanded = [parent for parent in expanded if parent.state != 0]
    
    #return expanded
    return tuple(expanded)    
    
#breath first search method       
def bfs(node):
    #Final state
    final = goal(node.state)
    #Declare frontier
    frontier = collections.deque()
    frontier.append(node)
    #Explored node and frontier nodes
    explored = set()
    nodes_expanded = 0
    max_fringe_size = 0
    max_depth = 0
    
    while True:
        #Node to test
        actual = frontier.pop()
        #Fringe size
        fringe_size = len(frontier)
        #Max search depth
        if actual.depth > max_depth:
            max_depth = actual.depth
        
        #Check if goal is reached
        if actual.state == final:
            #Backtrack path to parent
            final = actual
            path = []
            while True:
                #Check if root node
                if actual.depth == 0:
                    break
                path.insert(0, actual.move)
                actual = actual.parent
            return path, final, nodes_expanded, fringe_size, max_fringe_size, max_depth+1
        
        #Add explored node to explored set
        explored.add(actual.state)
        #Expand node
        for i in expand(actual):
            #Check if new nodes have been explored or already in frontier
            if i.state not in explored:
                #Order frontier for BFS
                frontier.appendleft(i)
                explored.add(i.state)
        #Number of expanded nodes
        nodes_expanded = nodes_expanded + 1
        #Max frontier size
        if len(frontier) > max_fringe_size:
            max_fringe_size = len(frontier)
        
    return 0

#depth first search method
def dfs(node):
    #Final state
    final = goal(node.state)
    #Declare frontier
    frontier = collections.deque()
    frontier.append(node)
    #Explored node and frontier nodes
    explored = set()
    nodes_expanded = 0
    max_fringe_size = 0
    max_depth = 0
    
    while True:
        #Node to test
        actual = frontier.popleft()
        #Fringe size
        fringe_size = len(frontier)
        #Max search depth
        if actual.depth > max_depth:
            max_depth = actual.depth
        
        #Check if goal is reached
        if actual.state == final:
            #Backtrack path to parent
            final = actual
            path = []
            while True:
                #Check if root node
                if actual.depth == 0:
                    break
                path.insert(0, actual.move)
                actual = actual.parent
            return path, final, nodes_expanded, fringe_size, max_fringe_size, max_depth, 0
        
        #Add explored node to explored set
        explored.add(actual.state)
        #Auxiliar stack
        aux = collections.deque()
        #Expand node
        for i in expand(actual):
            if i.state not in explored:
                aux.append(i)
                explored.add(i.state)
        #Order frontier for DFS
        aux.reverse()
        for i in aux:
            frontier.appendleft(i)
        #Number of expanded nodes
        nodes_expanded = nodes_expanded + 1
        #Max frontier size
        if len(frontier) > max_fringe_size:
            max_fringe_size = len(frontier)
            
    return 0

#RAM usage in MB
def memory():
    #For Linux based
    if os.name == 'posix':
        import resource
        return float(resource.getrusage(resource.RUSAGE_SELF).ru_maxrss / 1024)
    #For Windows
    else:
        import psutil
        p = psutil.Process()
        return float(p.memory_info().rss / (1024 * 1024))

#txt output    
def txtout(path, cost, nodes_expanded, fringe_size, max_fringe_size, depth, max_depth, t_total, mem):
    f = open("output.txt", "w+")
    f.write("path_to_goal: " + str(path))
    f.write("\ncost_of_path: " + str(cost))
    f.write("\nnodes_expanded: " + str(nodes_expanded))
    f.write("\nfringe_size: " + str(fringe_size))
    f.write("\nmax_fringe_size: " + str(max_fringe_size))
    f.write("\nsearch_depth: " + str(depth))
    f.write("\nmax_search_depth: " + str(max_depth))
    f.write("\nrunning_time: " + str(t_total))
    f.write("\nmax_ram_usage: "+ str(mem))
    f.close()

#Command line execution    
def main():
    #Initial time
    t_ini = time.time()  
    #Method chosen
    method = sys.argv[1]
    #Initial state
    initial = sys.argv[2]
    
    #Execute bfs 
    if method == "bfs":
        ini_state = [int(x) for x in initial.split(',')]
        ini_state = tuple(ini_state)
        ini_node = Node(ini_state, 0, None, None, 0)
        t = bfs(ini_node)
    
    #Execute dfs    
    if method == "dfs":
        ini_state = [int(x) for x in initial.split(',')]
        ini_state = tuple(ini_state)
        ini_node = Node(ini_state, 0, None, None, 0)
        t = dfs(ini_node)
        
    #Memory used 
    mem = memory()
    #Final time 
    t_end = time.time()
    #Total time
    t_total = t_end - t_ini
    #Text output document
    txtout(t[0], t[1].cost, t[2], t[3], t[4], t[1].depth, t[5], t_total, mem)

#Pythonism
if __name__ == "__main__":
    main()
