# напиши здесь свое приложение
from instructions import txt_instruction as t_x
from instructions import txt_test1
from instructions import txt_sits
from instructions import txt_test3

from ruffier import test

from kivy.app import App
from kivy.uix.screenmanager import ScreenManager, Screen
from kivy.uix.boxlayout import BoxLayout
from kivy.uix.button import Button
from kivy.uix.label import Label
from kivy.uix.textinput import TextInput

name1 = ''
name2 = ''
name3 = ''
name4 = ''
name5 = ''

from seconds import Seconds

def check_int(number):
    try:
        return int(number)
    except:
        return False

class ScrButton(Button):
    def __init__(self, screen, direction, goal, **kwargs):
        super().__init__(**kwargs)
        self.screen = screen
        self.direction = direction
        self.goal = goal

    def on_press(self):
        self.screen.manager.transition.direction = self.direction
        self.screen.manager.current = self.goal

class MainScreen(Screen):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        global name1
        global name2

        h_line = BoxLayout(orientation = 'vertical', padding = 8, spacing = 8)
        label = Label(text = t_x)
        h_line.add_widget(label)

        v_line_1 = BoxLayout(size_hint = (0.8, None), height = '30sp')
        label_1 = Label(text = 'Возраст:', pos_hint = {'center_x': 0.1})
        v_line_1.add_widget(label_1)
        self.textinput_1 = TextInput(text = '0', focus = False, multiline = False)
        v_line_1.add_widget(self.textinput_1)
        h_line.add_widget(v_line_1)

        v_line_2 = BoxLayout(size_hint = (0.8, None), height = '30sp')
        label_2 = Label(text = 'Имя:', pos_hint = {'center_x': 0.1})
        v_line_2.add_widget(label_2)
        self.textinput_2 = TextInput(text = '_', multiline = False)
        v_line_2.add_widget(self.textinput_2)
        h_line.add_widget(v_line_2)

        self.bt = Button(text = 'Начать', size_hint = (1, 0.2))
        self.bt.on_press = self.next
        h_line.add_widget(self.bt)

        name1 = self.textinput_1.text             
        name2 = self.textinput_2.text          
        self.add_widget(h_line)

    def next(self):
        name = self.textinput_2.text
        age = check_int(self.textinput_1.text)

        if age == False or age < 7:
            age = 7
            self.textinput_1.text = str(age)
        else:
            self.manager.current = 'a'


class Screen2(Screen):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        h_line = BoxLayout(orientation='vertical', padding=8, spacing=8)

        label = Label(text=txt_test1, size_hint=(1, 0.4))
        h_line.add_widget(label)

        self.timer = Seconds(15)
        h_line.add_widget(self.timer)

        v_line = BoxLayout(size_hint=(0.8, None), height='30sp')
        v_line.add_widget(Label(text='Результат:', halign='right'))
        self.textinput = TextInput(text='0', multiline=False)
        v_line.add_widget(self.textinput)
        h_line.add_widget(v_line)

        self.btn = Button(text='Начать', size_hint=(1, 0.2))
        self.btn.on_press = self.start_timer
        h_line.add_widget(self.btn)

        self.add_widget(h_line)

        self.timer.bind(done=self.timer_finished)

    def start_timer(self):
        self.btn.disabled = True
        self.timer.start()

    def timer_finished(self, *args):
        self.btn.text = 'Далее'
        self.btn.disabled = False
        self.btn.on_press = self.next

    def next(self):
        P1 = check_int(self.textinput.text)
        if P1 == False:
            self.textinput.text = 'Введите число'
        else:
            self.manager.current = 'b'


class Screen3(Screen):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        h_line = BoxLayout(orientation='vertical', padding=8, spacing=8)

        label = Label(text=txt_sits)
        h_line.add_widget(label)

        self.timer = Seconds(45)
        h_line.add_widget(self.timer)

        self.btn = ScrButton(self, text='Начать', direction='left', goal='c', size_hint=(1, 0.4))
        h_line.add_widget(self.btn)

        self.add_widget(h_line)

        self.timer.bind(done=self.timer_finished)
        self.btn.on_press = self.start_timer

    def start_timer(self):
        self.btn.text = 'Ждите...'
        self.btn.disabled = True
        self.timer.start()

    def timer_finished(self, *args):
        self.btn.text = 'Продолжить'
        self.btn.disabled = False
        self.btn.on_press = self.next

    def next(self):
        self.manager.current = 'c'

class Screen4(Screen):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.stage = 0

        h_line = BoxLayout(orientation='vertical', padding=8, spacing=8)
        self.label = Label(text='Считайте пульс')
        h_line.add_widget(self.label)

        self.timer = Seconds(15)
        h_line.add_widget(self.timer)

        v_line1 = BoxLayout(size_hint=(0.8, None), height='30sp')
        v_line1.add_widget(Label(text='Результат:', halign='right'))
        self.textinput3 = TextInput(text='0', multiline=False)
        v_line1.add_widget(self.textinput3)
        h_line.add_widget(v_line1)

        v_line2 = BoxLayout(size_hint=(0.8, None), height='30sp')
        v_line2.add_widget(Label(text='После отдыха:', halign='right'))
        self.textinput4 = TextInput(text='0', multiline=False)
        v_line2.add_widget(self.textinput4)
        h_line.add_widget(v_line2)

        self.btn = ScrButton(self, text='Начать', direction='left', goal='d', size_hint=(1, 0.3))
        h_line.add_widget(self.btn)

        self.add_widget(h_line)

        self.textinput3.disabled = True
        self.textinput4.disabled = True

        self.btn.on_press = self.start_timer
        self.timer.bind(done=self.next_stage)

    def start_timer(self):
        if self.stage == 0:
            self.btn.disabled = True
            self.timer.start()
            self.label.text = 'Считайте пульс (15 сек)'
        elif self.stage == 2:
            self.manager.current = 'd'

    def next_stage(self, *args):
        if self.timer.done:
            if self.stage == 0:
                self.stage = 1
                self.textinput3.disabled = False
                self.label.text = 'Отдыхайте'
                self.timer.restart(30)
            elif self.stage == 1:
                self.stage = 2
                self.label.text = 'Считайте пульс (15 сек)'
                self.timer.restart(15)
                self.textinput4.disabled = False
            elif self.stage == 2:
                self.btn.text = 'Завершить'
                self.btn.disabled = False

    def next(self):
        P2 = check_int(self.textinput3.text)
        P3 = check_int(self.textinput4.text)

        if P2 != False and P3 != False:
            self.manager.current = 'd'
        else:
            print(type(P2))
            print(type(P3))
            P2 = 'Введите число'
            self.textinput3.text = str(P2)
            P3 = 'Введите число'
            self.textinput4.text = str(P3)

class Screen5(Screen):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.instr = Label(text='Результат:')
        h_line = BoxLayout(orientation='vertical', padding=8, spacing=8)
        h_line.add_widget(self.instr)
        self.btn = ScrButton(self, text='Закончить', direction='left', goal='main', size_hint=(1, 0.4))
        h_line.add_widget(self.btn)
        self.add_widget(h_line)

    def on_enter(self):  
        self.before()

    def before(self):
        screen4 = self.manager.get_screen('c')
        screen1 = self.manager.get_screen('a')

        p1 = check_int(screen1.textinput.text)
        p2 = check_int(screen4.textinput3.text)
        p3 = check_int(screen4.textinput4.text)
        age = check_int(self.manager.get_screen('main').textinput_1.text)

        if not p1 or not p2 or not p3 or not age:
            self.instr.text = "Ошибка: введите корректные данные"
        else:
            result_str = test(p1, p2, p3, age)
            self.instr.text = result_str


class MyApp(App):
    def build(self):
        sc = ScreenManager()
        sc.add_widget(MainScreen(name = 'main'))
        sc.add_widget(Screen2(name = 'a'))
        sc.add_widget(Screen3(name = 'b'))
        sc.add_widget(Screen4(name = 'c'))
        sc.add_widget(Screen5(name = 'd'))

        return sc

MyApp().run()
