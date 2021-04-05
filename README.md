import csv
import time
start_time = time.time()
def translate():
  f = open("french_dictionary.csv", "r")
  csv_reader = csv.reader(f)
  m=0
  with open('frequency.csv', mode='w') as e:
    em= csv.writer(e, delimiter=',')
    for x in csv_reader:
      k=0
      m+=1
      with open('t8.shakespeare.txt', 'r+') as file :
        for line in file:
          punc = '''!()-[]{};:'"\,<>./?@#$%^&*_~'''
          for ele in line: 
            if ele in punc: 
              line = line.replace(ele, "")
          words = line.split()
          for i in words:
            if(i==x[0]):
              k+=1
      with open('t8.shakespeare.txt', 'r') as file:
        filedata = file.read()
      filedata = filedata.replace(x[0],x[1])
      with open('t8.shakespeare.txt', 'w') as file:
        file.write(filedata)
      em.writerow([x[0],x[1],k])
translate()
print(time.time() - start_time)
