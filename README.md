# Python-Project-
This is my Python project.
from dataclasses import dataclass, asdict
from typing import List
import pickle
import os
from sys import exit

@dataclass
class Patient:
    name: str
    age: int
    problem: str
    phone: int
    id: str

@dataclass
class Doctor:
    name: str
    age: int
    department: str
    phone: int
    id: str

@dataclass
class Worker:
    name: str
    age: int
    work: str
    phone: int
    id: str

DATA_FILE = 'data_Hospital.pkl'

def load_data():
    if os.path.exists(DATA_FILE):
        with open(DATA_FILE, 'rb') as f:
            return pickle.load(f)
    else:
        return {'patients': [], 'doctors': [], 'workers': []}

def save_data(data):
    with open(DATA_FILE, 'wb') as f:
        pickle.dump(data, f)

def find_by_id(collection: List, id_value: str):
    for item in collection:
        if item.id == id_value:
            return item
    return None

def delete_by_id(collection: List, id_value: str):
    for i, item in enumerate(collection):
        if item.id == id_value:
            del collection[i]
            return True
    return False

def main():
    data = load_data()
    print("======== HOSPITAL MANAGEMENT SYSTEM ============")
    print("1.LOGIN")
    print("2.EXIT")
    choice = int(input("ENTER YOUR CHOICE: "))
    if choice == 1:
        u1 = input("Enter user name: ")
        pwd1 = input("Enter the password: ")
        if u1 == 'VITB' and pwd1 == 'VITB@123':
            print("Login Successfull!")
            while True:
                print("\n==== WELCOME TO HOSPITAL MANAGEMENT AREA ====")
                print("\n1.Register Patient")
                print("2.Register Doctor")
                print("3.Register Worker")
                print("4.Show all Patients")
                print("5.Show all Doctors")
                print("6.Show all Workers")
                print("7.Show Patient by ID")
                print("8.Show Doctor by ID")
                print("9.Show Worker by ID")
                print("10.Update Patient Problem")
                print("11.Update Doctor Department")
                print("12.Update Worker Work")
                print("13.Delete Record by ID")
                print("14.Exit")
                choice = int(input("\nENTER YOUR CHOICE: "))

                if choice == 1:
                    pname = input("Enter Patient Name: ")
                    page = int(input("Enter Age: "))
                    pproblem = input("Enter Problem/Disease: ")
                    pphone = int(input("Enter Phone number: "))
                    pid = input("Enter Patient ID: ")
                    patient = Patient(pname, page, pproblem, pphone, pid)
                    data['patients'].append(patient)
                    save_data(data)
                    print("Patient successfully registered.")

                elif choice == 2:
                    dname = input("Enter Doctor Name: ")
                    dage = int(input("Enter Age: "))
                    ddept = input("Enter Department: ")
                    dphone = int(input("Enter Phone number: "))
                    did = input("Enter Doctor ID: ")
                    doctor = Doctor(dname, dage, ddept, dphone, did)
                    data['doctors'].append(doctor)
                    save_data(data)
                    print("Doctor successfully registered.")

                elif choice == 3:
                    wname = input("Enter Worker Name: ")
                    wage = int(input("Enter Age: "))
                    wwork = input("Enter type of Work: ")
                    wphone = int(input("Enter Phone number: "))
                    wid = input("Enter Worker ID: ")
                    worker = Worker(wname, wage, wwork, wphone, wid)
                    data['workers'].append(worker)
                    save_data(data)
                    print("Worker successfully registered.")

                elif choice == 4:
                    print("List of Patients:")
                    for p in data['patients']:
                        print(asdict(p))

                elif choice == 5:
                    print("List of Doctors:")
                    for d in data['doctors']:
                        print(asdict(d))

                elif choice == 6:
                    print("List of Workers:")
                    for w in data['workers']:
                        print(asdict(w))

                elif choice == 7:
                    pid = input("Enter Patient ID: ")
                    patient = find_by_id(data['patients'], pid)
                    if patient:
                        print(asdict(patient))
                    else:
                        print("Patient not found.")

                elif choice == 8:
                    did = input("Enter Doctor ID: ")
                    doctor = find_by_id(data['doctors'], did)
                    if doctor:
                        print(asdict(doctor))
                    else:
                        print("Doctor not found.")

                elif choice == 9:
                    wid = input("Enter Worker ID: ")
                    worker = find_by_id(data['workers'], wid)
                    if worker:
                        print(asdict(worker))
                    else:
                        print("Worker not found.")

                elif choice == 10:
                    pid = input("Enter Patient ID: ")
                    patient = find_by_id(data['patients'], pid)
                    if patient:
                        new_problem = input("Enter the new Problem/Disease: ")
                        patient.problem = new_problem
                        save_data(data)
                        print("Patient data updated.")
                    else:
                        print("Patient not found.")

                elif choice == 11:
                    did = input("Enter Doctor ID: ")
                    doctor = find_by_id(data['doctors'], did)
                    if doctor:
                        new_dept = input("Enter the new Department: ")
                        doctor.department = new_dept
                        save_data(data)
                        print("Doctor data updated.")
                    else:
                        print("Doctor not found.")

                elif choice == 12:
                    wid = input("Enter Worker ID: ")
                    worker = find_by_id(data['workers'], wid)
                    if worker:
                        new_work = input("Enter the new Work type: ")
                        worker.work = new_work
                        save_data(data)
                        print("Worker data updated.")
                    else:
                        print("Worker not found.")

                elif choice == 13:
                    print("Delete Record by: ")
                    print("1.Patient")
                    print("2.Doctor")
                    print("3.Worker")
                    del_choice = int(input("Enter choice: "))
                    if del_choice == 1:
                        pid = input("Enter Patient ID to delete: ")
                        if delete_by_id(data['patients'], pid):
                            save_data(data)
                            print("Patient record deleted.")
                        else:
                            print("Patient not found.")
                    elif del_choice == 2:
                        did = input("Enter Doctor ID to delete: ")
                        if delete_by_id(data['doctors'], did):
                            save_data(data)
                            print("Doctor record deleted.")
                        else:
                            print("Doctor not found.")
                    elif del_choice == 3:
                        wid = input("Enter Worker ID to delete: ")
                        if delete_by_id(data['workers'], wid):
                            save_data(data)
                            print("Worker record deleted.")
                        else:
                            print("Worker not found.")
                    else:
                        print("Invalid choice.")

                elif choice == 14:
                    print("Exiting...")
                    exit()

                else:
                    print("Invalid choice, please try again.")
        else:
            print("Wrong username/password.")
            print("Exiting...")
    elif choice == 2:
        print("Exiting...")
        print("Thanks for using Hospital Management system ! ")
        exit()
    else:
        print("Invalid choice.")

if __name__ == "__main__":
    main()
