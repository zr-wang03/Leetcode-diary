# UTEK Programming II

### Part 2&#x20;

```
#-------------------------------------------------------------------------------
# Name:         Part2
# Purpose:      UTEK Programming
#
# Author:       LinQiao Zhang, Zhuoran Wang
#
# Created:     15/01/2022
# Copyright:(c) LinQiao Zhang, Zhuoran Wang
#-------------------------------------------------------------------------------

def main():
    print("\n File Options: \n")
    print("|  1a.in.txt  |  2a.in.txt  |  3a.in.txt  |  4a.in.txt  |  5a.in.txt  |")
    print("|  1b.in.txt  |  2b.in.txt  |  3b.in.txt  |  4b.in.txt  |  5b.in.txt  |")
    print("|  1c.in.txt  |  2c.in.txt  |  3c.in.txt  |  4c.in.txt  |  5c.in.txt  |")

    filename=input("\nPlease enter file name: ")
    file=filereader(filename)
    fileeditor(file,filename)
    path=findpath()
    output_path(path,filename)


def output_path(path,filename):
    curr=(0,0)
    output_name=filename[:2]+".out.txt"
    with open(output_name,"w") as fp:
        fp.write("Robot "+name[0]+"\n")
        for i in path:
            fp.write(printpath(curr,i))
            fp.write("clean "+str(i[0])+" "+str(i[1])+"\n")
            curr=i
        fp.write("rest")
    print("Output complete \n\nSee 'UTEK programming Part2' folder\n")


def filereader(filename):
    with open(filename,"r") as fp:
        ans=[]
        line = fp.readline()
        cnt = 0
        #cnt stores the number of lines in the document
        while line:
            ans.append(line)
            line = fp.readline()
            cnt += 1
        #use the following for loop to get rid of the "\n" at the end of the lines
        for i in range(cnt-1):
            ans[i]=ans[i][:-1]

        return ans


def fileeditor(file,filename):
    global number_robot,number_location,number_obsatcle,name,moveEff,cleanEff,location, obstacle
    #print(file)
    #The first line contains the following: (num of robots, numb of locations, num of obstacles)
    information=file[0]
    temp=information.split()
    number_robot=int(temp[0])
    number_location=int(temp[1])
    number_obsatcle=int(temp[2])

    #the second line contains the following information:(name, moveEff, cleanEff)
    name=[]*number_robot
    moveEff=[]*number_robot
    cleanEff=[]*number_robot
    #print (name,moveEff,cleanEff)
    for i in range(number_robot):
        #print(i)
        name_temp=file[1+i]
        temp=name_temp.split()
        #print(temp)
        name.append(temp[0])
        moveEff.append(int(temp[1]))
        cleanEff.append(int(temp[2]))

    #print (name,moveEff,cleanEff)

    #use a dictionary to get the locations and also its values, if we see an location that is already in the dic,we update it
    location={}
    for i in range(number_location):
        loc_temp=file[i+number_robot+1]
        temp=loc_temp.split()
        loc=(int(temp[0]),int(temp[1]))
        loc_time=int(temp[2])
        if loc in location:
            location[loc]=max(location[loc],loc_time)
        else:
            location[loc]=loc_time
    #print (location)

    #get the obstacles as tuples for further use

    obstacle=[]
    for i in range(number_obsatcle):
        obs_temp=file[i+number_robot+number_location+1]
        temp=obs_temp.split()
        obs=(int(temp[0]),int(temp[1]),int(temp[2]),int(temp[3]))
        obstacle.append(obs)


def distance(x,y):
    #The steps need to go from one position to another without obstacles
    # equal to the larger between horizontal distance and vertical distance
    dis_i=abs(x[0]-y[0])
    dis_j=abs(x[1]-y[1])
    return max(dis_i,dis_j)


def findpath():
    #for each location, we are looking for the nearest location that hasn't been visited
    path=[]
    curr=(0,0)
    i=0
    while i<=number_location:
        mini=float('inf')
        minj=(0,0)
        for j in location.keys():
            if j not in path:
                curr_dis=distance(curr,j)
                if curr_dis<mini:
                    mini=curr_dis
                    minj=j
        path.append(minj)
        i+=1
    return path

def printpath(x,y):
    i,j=x[0],x[1]
    i_a,j_a=y[0],y[1]
    ans=""
    while i!=i_a or j_a!=j:
        if i!=i_a:
            i+=abs(i_a-i)//(i_a-i)
        if j!=j_a:
            j+=abs(j_a-j)//(j_a-j)
        ans=ans+"move "+str(i)+" "+str(j)+"\n"
    return ans









if __name__ == '__main__':
    main()

```

{% file src="../.gitbook/assets/2a.in.txt" %}

{% file src="../.gitbook/assets/2b.in.txt" %}

{% file src="../.gitbook/assets/2c.in.txt" %}
