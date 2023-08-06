# Chapter 10 : Classes

날짜: 2023년 6월 18일 → 2023년 6월 24일
요약: _"클래스도 함수처럼 쪼개고 쪼개자(\*)."_ 단, 기능(responsibility) 단위여야 한다.

## Class Organization

- 클래스 시작은 변수 목록으로: Public static constants > Private static variables > Private instance variables 순서대로
- Public functions > Private utilities called by a public function 방식으로 함수를 정의하면 그에 호출하는 것들이 바로 뒤따라오는 구조여야 읽기 편하다.

## Classes Should be Small!!

- 포함하는 methods의 갯수가 많고 적고를 떠나 한 가지 기능을 하게끔 쪼갠다.
- 그래서 클래스 이름이 간결해야 한다; if, and, or, 또는 but이 사용되어야 온전한 설명이 가능하다면 한 가지 보다 더 많은 기능 역할을 하는 증거이다.

## The Single Responsibility Principle (SRP)

- OO desgin에서 중요한 개념이지만 가장 쉽게 훼손되는 원칙이기도 하다.
- 클래스나 모듈이 단 하나의 reason to change (i.e., responsibility)를 가져야 한다.
- _Getting software to work and making software clean are two very different activities._ 기능 구현에 초점을 맞추다 클린코드를 잊는다. 동작하게 만드는 것만큼 깔끔하게 유지하는 것도 중요하다.
- 작은 클래스를 많이 만든다고 큰 클래스 몇 개보다 더 많은 moving parts가 생기지 않는다. 크고 복잡하게 만드는 것으로 성취감을 쌓지 말자.
- 복잡도를 다루는데는 어디에 무엇이 있는지 찾기 좋게 만드는 것이 우선이다; Make _each small class encapsulates a single responsibility, has a single reason to change, and collaborates with a few others to achieve the desired system behaviours_.

## Cohesion (응집도)

- high cohesion = 클래스 안에 methods & variables are co-dependent

## Maintaining Cohesion Results in Many Small Classes

- 클래스 크기 쪼개기는 a proliferation (분열 증식, 확산) of classes를 만들고 low cohesion을 만든다. 몇몇 소수 함수가 특정 변수를 공유하게 된다면 그 자체로 클래스를 따로 구성하게 쪼개는 것이 좋다: low cohesion -> split the class.
- net-listed 코드 작성을 피하고 클래스, 함수, 변수 각각에 명확한 이름을 부여할 수 있게 작은 단위로 쪼개자.
- refactoring 예제가 오리지널 코드 보다 길어지는 이유: 1) 더 길고 더 자세히 지어진 변수 이름, 2) 마치 주석을 쓰는 것처럼 작성된 함수와 클래스 선언, 3) 읽기 쉽게 하기 위한 whitespace와 formatting techiques 사용하기 때문이다.
- refactoring is "not start over from scratch and write the program over again", 테스트에 맞게 "정확한(precise)" 기능을 하나씩 담당하게 class를 구성한다.

## Organizing for Change

- _"새 기능을 추가할 때 시스템을 확장할 뿐 기존 코드를 변경하지 않는 게 이상적인 시스템(\*)"_ 이다.
- SRP를 잊지말자. 그리고 주요 객체지향 클래스 디자인에는 Open-Closed Principle(OCP)도 있다; _Classes should be open for extension but closed for modification_.

## Isolating from Change

- 코드는 변하는 목적에 따라 바뀌게 될 것이다.
- concrete class (_"구체적인 클래스"(\*)_)가 API 호출 등의 이유로 리턴 값이 변한다면 _"인터페이스와 추상 클래스를 통해 구현이 미치는 영향을 격리하는게 좋다"(\*)_
- Dependency Inversion Principle (DIP)는 _classes should depend upon abstractions, not on concrete details_ 을 말한다.

## Example: how to refactor the class? -> follow up action! Chapter 16

```python
class Calculate():
    def __init__(self, specialty):
        self.specialty = specialty
        self.w1 = list(self.specc_df['SpecComm % Contribution Limited'])
        self.w2 = list(self.specc_df['w2'])
        ...

    def method(self):
        method = 1
        if self.specialty == 'General Practice' or self.specialty == 'Public Health Medicine':
            method = 4
        elif self.specialty == 'Obstetrics and gynaecology' or self.specialty == 'Community Sexual and Reproductive Health':
            method = 2
        elif search('Psych', self.specialty):
            method = 3
        return method

    def f1(self):
        self.specc_df['specc dist'] = (self.specc_df['IP SpecComm %']*0.5) + (self.specc_df['OP SpecComm %']*0.5)

        return self.specc_df[['Specialty', '2019 CCG Name', 'specc dist']]

    ...

    def f3(self):
        if self.specialty == 'General Practice' or self.specialty == 'Public Health Medicine':
            self.hee_df['hee dist'] = self.hee_df['IP OP Combined Distribution SMR<75 Index 20']
        else:
            self.hee_df['hee dist'] = (self.hee_df['IP Dist SMR<75 Index 20']*0.5) + (self.hee_df['OP Dist SMR<75 Index 20']*0.5)

        return self.hee_df[['2019 CCG Name', 'hee dist']]

    def guided_dist(self):
        specc = self.f1()
        nhsei = self.f2()
        hee = self.f3()
        guided_df = (specc.merge(nhsei, on='2019 CCG Name')).merge(hee, on='2019 CCG Name')
        guided_df['w1'] = self.w1
        guided_df['w2'] = self.w2
        guided_df['guided dist'] = (guided_df['specc dist']*guided_df['w1']) + ((guided_df['nhsei dist']*0.5+guided_df['hee dist']*0.5)*guided_df['w2'])

        return guided_df

class Output():
    def __init__(self):
        self.specialties = args.specialties
        self.output_df = pd.DataFrame()

    def file(self):
        if self.department is None and self.specialties is None:
            for spec in self.specialties_full:
                guided_df = Calculate(specialty=spec).guided_dist()
                self.output_df = pd.concat([self.output_df, guided_df])
            tests = self.tests()
            if tests[0]:
                self.output_df.to_csv(str(c.output_dir / 'final_guided_dist.csv'), index=False)
                print('Your output csv file is ready and has passed the checks, thank you.')
                return
            else:
                self.output_df.to_csv(str(c.output_dir / 'final_guided_dist.csv'), index=False)
                print('The output has failed for reason {}, please check your input files.'.format(tests[1]))
                return

        elif self.department is None:
            for spec in self.specialties.split(', '):
                if spec not in self.specialties_full:
                    print('You have entered at least one invalid specialty or department, please retry.')
                    return
                ...

        else:


    def tests(self):
        if sorted(list(self.output_df['2019 CCG Name'].unique())) != sorted(self.ccg_list):
            return (False, 1)
        if self.specialties is not None and len(list(self.output_df['Specialty'].unique())) != len(self.specialties.split(', ')):
            return (False, 2)
        if len(self.output_df)%191 != 0:
            return (False, 3)
        if abs(sum(self.output_df['guided dist']) - len(list(self.output_df['Specialty'].unique()))) > 0.00001:
            return (False, 4)
        else:
            return (True, 0)


if __name__ == "__main__":
    Output().file()
```

(\*)한글 문구 출처: 무해님의 네이버 블로그 기록, "[클린코드] 10.클래스", https://blog.naver.com/cookr3/223077399469
