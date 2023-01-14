import os

class TodoList:
    def __init__(self):
        #create data file
        self.file_path = "./data.txt"
        directory = os.path.dirname(self.file_path)
        if not os.path.exists(directory):
            os.makedirs(directory)

        self.read_data()
        self.create_todo()
        self.loop()

    def loop(self):
        user_input = ''
        self.list_todo()
        while user_input != 'N':
            user_input = self.handle_input()
            self.convert_dict()
            self.save_data()
            self.read_data()
            self.list_todo()

    def read_data(self):
        with open(self.file_path, "r") as f:
            self.file = f.readlines()

    def create_todo(self):
        self.todo_dict = {
            'priority':{
                '1':{},
                '2':{},
                '3':{}
            }
        }
        for i in self.file:
            priority = i.split(' ')[5].split('\n')[0]
            name = i.split(' ')[0]
            time = i.split(' ')[3].split(',')[0]
            self.todo_dict['priority'][priority][name] = time

    def list_todo(self):
        todo = ''
        for i in self.file:
            todo = todo + i
        if todo != '':
            print('--------------------------------------------\n'+todo+'--------------------------------------------')  
        else:
            print('--------------------------------------------\n'+'Nothing to see here\n'+'--------------------------------------------')

    def convert_dict(self):
        self.todo_file = ''
        for x in self.todo_dict['priority'].keys():
            for key,value in self.todo_dict['priority'][x].items():
                self.todo_file = self.todo_file + f'{key} : due {value}, priority {x}\n'

    def save_data(self):
        with open(self.file_path, "w") as f:
            f.truncate(0)
            f.write(self.todo_file)

    def handle_input(self):
        #handle input functions
        func_name = input('Functions - add,remove,change,clear : ')
        if func_name == 'add':
            priority = input('priority of this project (1 to 3) : ')
            name = input('Name of this project : ')
            time = input('due time of this project (template : YYYY\MM\DD) : ')
            #create dict
            self.todo_dict['priority'][priority][name] = time
        elif func_name == 'remove':
            priority = input('priority of this project (1 to 3) : ')
            name = input('Name of this project : ')
            #remove dict
            del self.todo_dict['priority'][priority][name]
        elif func_name == 'change':
            priority = input('priority of this project (1 to 3) : ')
            name = input('Name of this project : ')
            #change existing values
            new_priority = input('priority of this project (1 to 3) or write same : ')
            new_name = input('Name of this project or write same : ')
            new_time = input('due time of this project (template : YYYY\MM\DD) or write same : ')
            #check if its the same
            if new_priority == 'same': 
                new_priority = priority
            if new_name == 'same': 
                new_name = name
            if new_time == 'same': 
                new_time = self.todo_dict['priority'][priority][name]
            #delete old, create new dict
            del self.todo_dict['priority'][priority][name]
            self.todo_dict['priority'][new_priority][new_name] = new_time

        elif func_name == 'clear':
            #delete everything from data
            with open(self.file_path, "w") as f:
                f.truncate(0)
            self.todo_dict['priority'] = {'1':{},
                                        '2':{},
                                        '3':{}}
        
        else: func_name = 'N'
        return func_name

if __name__ == '__main__':
    TodoList()