import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { useState } from "react";

export default function Home() {
  const [students, setStudents] = useState([]);
  const [name, setName] = useState("");
  const [amount, setAmount] = useState("");

  const handleSubmit = () => {
    if (!name || !amount) return;
    const newEntry = { name, amount: parseFloat(amount), date: new Date().toLocaleDateString() };
    setStudents([...students, newEntry]);
    setName("");
    setAmount("");
  };

  const totalAmount = students.reduce((acc, s) => acc + s.amount, 0);

  return (
    <div className="min-h-screen bg-gradient-to-b from-green-100 to-green-300 p-4">
      <div className="text-center mb-6">
        <h1 className="text-3xl font-bold text-green-900">ইসলামিক ছাত্র সঞ্চয় অ্যাপ</h1>
        <p className="text-green-700">ছাত্রদের জন্য নিরাপদ ও সহজ সঞ্চয়ের ডিজিটাল সমাধান</p>
      </div>

      <Card className="max-w-md mx-auto mb-6 shadow-xl">
        <CardContent className="p-4 space-y-4">
          <Input placeholder="নাম লিখুন" value={name} onChange={(e) => setName(e.target.value)} />
          <Input placeholder="টাকার পরিমাণ (৳)" type="number" value={amount} onChange={(e) => setAmount(e.target.value)} />
          <Button onClick={handleSubmit} className="w-full bg-green-600 hover:bg-green-700 text-white">জমা দিন</Button>
        </CardContent>
      </Card>

      <Card className="max-w-md mx-auto shadow-md">
        <CardContent className="p-4">
          <h2 className="text-xl font-semibold text-green-800 mb-2">মোট জমা: ৳{totalAmount}</h2>
          <ul className="space-y-2">
            {students.map((s, i) => (
              <li key={i} className="bg-white p-2 rounded shadow flex justify-between">
                <span>{s.name} - ৳{s.amount}</span>
                <span className="text-sm text-gray-500">{s.date}</span>
              </li>
            ))}
          </ul>
        </CardContent>
      </Card>
    </div>
  );
}
