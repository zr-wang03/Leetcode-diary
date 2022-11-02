# UTEK Programming I

{% file src="../.gitbook/assets/2022 programming competitor's package.pdf" %}

### Part one&#x20;

```
#-------------------------------------------------------------------------------
# Name:         Part1
# Purpose:      Given a file, this program aggregates the location and time required to clean the location, along with creating another .txt file (in the UTEK programming Part1 Folder) to store the outputs
#
# Author:       LinQiao Zhang, Zhuoran Wang, Victor Wang 
#
# Created:     15/01/2022
# Copyright:(c) LinQiao Zhang, Zhuoran Wang, Victor Wang
#-------------------------------------------------------------------------------

def main():
    print("\n File Options: \n")
    print("|  1a.in.txt  |  2a.in.txt  |  3a.in.txt  |  4a.in.txt  |  5a.in.txt  |")
    print("|  1b.in.txt  |  2b.in.txt  |  3b.in.txt  |  4b.in.txt  |  5b.in.txt  |")
    print("|  1c.in.txt  |  2c.in.txt  |  3c.in.txt  |  4c.in.txt  |  5c.in.txt  |")
    filename=input("\nPlease enter file name: ")
    file=filereader(filename)
    fileeditor(file,filename)

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

    #The required format looks like the following:
    #Robot Name: alpha; Movement Efficiency: 4; Cleaning Efficiency: 5;
    #Location Number: 1; Time required: 3; Location: 5 6;
    out_name=filename[:2]+".out.txt"
    with open(out_name,"w") as fp:
        fp.write("Robot Name: "+name[0]+"; Movement Efficiency: "+str(moveEff[0])+"; Cleaning Efficiency: "+str(cleanEff[0])+";\n")
        i=1
        for loc in location.keys():
            fp.write("Location Number: "+str(i)+"; Time required: "+str(location[loc])+"; Location: "+str(loc[0])+" "+str(loc[1])+";\n")
            i+=1
    print("Output complete \n\nSee 'UTEK programming Part1' folder\n")





if __name__ == '__main__':
    main()

```

{% file src="../.gitbook/assets/1a.in.txt" %}

{% file src="../.gitbook/assets/1b.in.txt" %}

{% file src="../.gitbook/assets/1c.in.txt" %}

{% file src="../.gitbook/assets/Part1REAME.txt" %}
