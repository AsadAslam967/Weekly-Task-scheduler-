class WeekTaskScheduler:
    def _init_(self):
        self.schedule = {
            'Monday': [],
            'Tuesday': [],
            'Wednesday': [],
            'Thursday': [],
            'Friday': [],
            'Saturday': [],
            'Sunday': []
        }

    def add_task(self, day, task):
        day = day.capitalize()
        if day in self.schedule:
            self.schedule[day].append(task)
            print("✅ Task added to {}.".format(day))
        else:
            print("❌ Invalid day. Please enter a valid weekday.")

    def view_tasks(self, day=None):
        if day:
            day = day.capitalize()
            if day in self.schedule:
                print("\n📅 Tasks for {}:".format(day))
                if self.schedule[day]:
                    for i, task in enumerate(self.schedule[day], 1):
                        print("  {}. {}".format(i, task))
                else:
                    print("  No tasks.")
            else:
                print("❌ Invalid day.")
        else:
            print("\n📆 Weekly Schedule:")
            for d, tasks in self.schedule.items():
                print("\n{}:".format(d))
                if tasks:
                    for i, task in enumerate(tasks, 1):
                        print("  {}. {}".format(i, task))
                else:
                    print("  No tasks.")

    def remove_task(self, day, index):
        day = day.capitalize()
        if day in self.schedule:
            if 0 < index <= len(self.schedule[day]):
                removed = self.schedule[day].pop(index - 1)
                print("🗑 Removed task: {}".format(removed))
            else:
                print("❌ Invalid task number.")
        else:
            print("❌ Invalid day.")

def main():
    scheduler = WeekTaskScheduler()

    while True:
        print("\n--- Weekly Task Scheduler ---")
        print("1. Add Task")
        print("2. View Tasks")
        print("3. Delete Task")
        print("4. Exit")

        choice = input("Choose an option (1-4): ")

        if choice == '1':
            day = input("Enter the day: ")
            task = input("Enter the task: ")
            scheduler.add_task(day, task)

        elif choice == '2':
            view_day = input("Enter day to view (leave empty for full week): ")
            scheduler.view_tasks(view_day if view_day else None)

        elif choice == '3':
            day = input("Enter the day to delete a task from: ")
            scheduler.view_tasks(day)
            try:
                index = int(input("Enter task number to delete: "))
                scheduler.remove_task(day, index)
            except ValueError:
                print("❌ Please enter a valid number.")

        elif choice == '4':
            print("👋 Exiting scheduler. Have a productive week!")
            break

        else:
            print("❌ Invalid option. Please choose between 1 and 4.")

if _name_ == "_main_":
    main()# Weekly-Task-scheduler-
