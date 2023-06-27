#include <LiquidCrystal.h>
#include <Wire.h>

#define vb 7
// LiquidCrystal lcd( 12, 11, 10, 9, 8,7);
LiquidCrystal lcd(8, 9, 10, 11, 12, 13);

#define splash splash1

#define buz A2
float tempfn, tu;

const int ACC = 0x68;  // I2C address of the MPU-6050
unsigned int AcX, AcY, AcZ;
int fStatus, f_Status;

int disp = 0;

void setup() {
  LcDSet();
  pinMode(vb, OUTPUT);
  pinMode(buz, OUTPUT);
  digitalWrite(buz, LOW);
  Serial.begin(9600);
  Wire.begin();
  Wire.beginTransmission(0x68);
  Wire.write(0x6B);  // PWR_MGMT_1 register
  Wire.write(0);     // set to zero (wakes up the MPU-6050)
  Wire.endTransmission(true);
  lcd.clear();
}
void LcDSet() {
  lcd.begin(16, 2);

  splash(0, "Dehydration");
  splash(1, "Monitoring");

  delay(2000);
}
void loop() {

  float temp = analogRead(A1);
  tempfn = ((5 * temp * 100) / 1023);
  int wat = analogRead(A0);
  int wat_fn = map(wat, 0, 1023, 0, 100);
  f_Status = getAcc();

  if (f_Status) {
    digitalWrite(buz, HIGH);
  } else {
    digitalWrite(buz, LOW);
  }
  Serial.println(wat);
  // if (tempfn < 0) {
  //   tempfn = tempfn + 57;
  // }

  if (tempfn >= 37.8) {
    digitalWrite(vb, HIGH);
    delay(50);
    digitalWrite(vb, LOW);
  }

  if (wat_fn >= 6
  0) {
    digitalWrite(vb, HIGH);
    delay(80);
    digitalWrite(vb, LOW);
  }

  disp++;
  if (disp > 3) {
    lcd.setCursor(0, 0);
    lcd.print("T: ");
    lcd.setCursor(2, 0);
    lcd.print(tempfn);
    lcd.setCursor(9, 0);
    lcd.print("S: ");
    lcd.setCursor(12, 0);
    lcd.print(wat_fn);
    disp = 0;
  }
  // Serial.println(tempfn);


  delay(100);
}

void splash1(int row, String txt) {
  int curs = (17 - txt.length()) / 2;
  lcd.setCursor(0, row);
  //  lcd.print("################");
  lcd.print("----------------");
  lcd.setCursor(curs, row);
  lcd.print(txt);
  delay(300);
}
void splash2(int row, String txt) {
  int curs = (21 - txt.length()) / 2;
  lcd.setCursor(0, row);
  lcd.print("--------------------");
  lcd.setCursor(curs, row);
  lcd.print(txt);
  delay(300);
}