# railwayreservation-zoho-python-
#this one is very basic program. make changes wherever needed before usage'
class railwayreservation():
    

    def __init__(self):
        self.id = 0
        self.passengers = {}
        self.seats = ['u_birth', 'l_birth', 'm_birth', 'rac', 'wlist']
        self.nseats = [1, 1, 1, 1, 1]
        self.noofseats = [0,0,0,0,0]

    def book(self,name,preferance):
        a = self.seats.index(preferance)
        if self.noofseats[a] < self.nseats[a]:
            self.name = name
            self.preferance = preferance
            self.id += 1
            self.noofseats[a] += 1
            self.allocation = preferance
            self.passengers[str(self.id)] = [self.name,self.preferance,self.allocation]
        elif self.noofseats[a] >= self.nseats[a]:
            for i in range(3):
                if self.noofseats[i] < self.nseats[i]:
                    self.name = name
                    self.preferance = preferance
                    self.id += 1
                    self.noofseats[i] += 1
                    self.allocation = self.seats[i]
                    self.passengers[str(self.id)] = [self.name, self.preferance, self.allocation]
                    return
            if self.noofseats[3] < self.nseats[3]:
                self.name = name
                self.preferance = preferance
                self.id += 1
                self.noofseats[3] += 1
                self.allocation = 'rac'
                self.passengers[str(self.id)] = [self.name, self.preferance, self.allocation]
            elif self.noofseats[4] < self.nseats[4]:
                self.name = name
                self.preferance = preferance
                self.id += 1
                self.noofseats[4] += 1
                self.allocation = 'wlist'
                self.passengers[str(self.id)]= [self.name, self.preferance, self.allocation]
            else:
                print(f'no seats available for {name}')


    def see(self):
        for i in self.passengers:
            print(f"passen.id = {i} ,name ={self.passengers[i][0]} , alloted = {self.passengers[i][2]}")
    def remaining(self):
        print("\n")
        print('Available seats are:')
        for i in range(5):
            q = self.nseats[i] - self.noofseats[i]
            print(f"{self.seats[i]} = {q}")
        print("\n")
    def cancel(self,id):
        w = (self.passengers[id])[-1]
        e = self.seats.index(w)
        self.noofseats[e] -= 1
        self.passengers.pop(id)
        self.count = 0
        for j in self.passengers:

            if (self.passengers[j][-1] == 'u_birth') or (self.passengers[j][-1] =='l_birth') or (self.passengers[j][-1] =='m_birth') :

                if self.passengers[j][-2] == self.passengers[j][-1]:
                    continue
                else:

                    r = self.seats.index(self.passengers[j][-2])
                    t = self.seats.index(self.passengers[j][-1])
                    if self.noofseats[r] < self.nseats[r]:
                        self.passengers[j][-1] = self.passengers[j][-2]
                        self.noofseats[r] += 1
                        self.noofseats[t] -= 1
            elif  self.passengers[j][-1] == 'rac':

                for i in range(3):
                    if self.noofseats[i] < self.nseats[i]:
                        self.passengers[j][-1] = self.seats[i]
                        self.noofseats[3] -= 1
                        self.noofseats[i] += 1
            elif self.passengers[j][-1] == 'wlist':
                if self.noofseats[3] < self.nseats[3]:
                    self.passengers[j][-1] = 'rac'
                    self.noofseats[3] += 1
                    self.noofseats[4] -= 1
        self.see()
