// schema.prisma

model Soldier {
  id        Int        @id @default(autoincrement())
  rank      String     // ยศ (เช่น พลทหาร, สิบเอก)
  firstName String
  lastName  String
  status    String     @default("ACTIVE") // สถานะ: พร้อม, ลา, ป่วย
  duties    DutySlot[] // ความสัมพันธ์: ทหาร 1 คน เข้าเวรได้หลายรอบ
}

model Location {
  id          Int        @id @default(autoincrement())
  name        String     // ชื่อจุดตรวจ (เช่น ป้อมหน้า, คลังอาวุธ)
  description String?
  duties      DutySlot[] // ความสัมพันธ์: 1 จุด มีคนมาเข้าเวรได้หลายรอบ
}

model DutySlot {
  id         Int      @id @default(autoincrement())
  startTime  DateTime // เวลาเริ่มเข้าเวร
  endTime    DateTime // เวลาออกเวร
  note       String?  // หมายเหตุ (เช่น เฝ้าระวังพิเศษ)
  
  soldier    Soldier  @relation(fields: [soldierId], references: [id])
  soldierId  Int
  
  location   Location @relation(fields: [locationId], references: [id])
  locationId Int
}
