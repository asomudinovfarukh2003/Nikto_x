Nikt o_x
Для улучшения жизнь 
// App.jsx
import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";

const sampleProducts = [
  { id: 1, name: "Чехол на сиденье", category: "авто", price: 1200 },
  { id: 2, name: "Брелок для ключей", category: "аксессуары", price: 300 },
  { id: 3, name: "Органайзер в багажник", category: "авто", price: 1500 },
  { id: 4, name: "Очки антибликовые", category: "аксессуары", price: 800 },
];

export default function App() {
  const [cart, setCart] = useState([]);
  const [filter, setFilter] = useState("all");

  const addToCart = (product) => {
    setCart([...cart, product]);
  };

  const filteredProducts =
    filter === "all"
      ? sampleProducts
      : sampleProducts.filter((p) => p.category === filter);

  return (
    <div className="p-6">
      <h1 className="text-3xl font-bold mb-4">
        Магазин аксессуаров и автотоваров
      </h1>

      <div className="mb-4">
        <Button onClick={() => setFilter("all")}>Все</Button>
        <Button onClick={() => setFilter("авто")} className="ml-2">
          Авто
        </Button>
        <Button onClick={() => setFilter("аксессуары")} className="ml-2">
          Аксессуары
        </Button>
      </div>

      <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
        {filteredProducts.map((product) => (
          <Card key={product.id} className="p-4">
            <CardContent>
              <h2 className="text-xl font-semibold">{product.name}</h2>
              <p className="text-gray-500">Цена: {product.price} ₽</p>
              <Button className="mt-2" onClick={() => addToCart(product)}>
                Добавить в корзину
              </Button>
            </CardContent>
          </Card>
        ))}
      </div>

      <div className="mt-8">
        <h2 className="text-2xl font-bold mb-2">Корзина</h2>
        {cart.length === 0 ? (
          <p className="text-gray-500">Корзина пуста</p>
        ) : (
          <ul className="list-disc pl-5">
            {cart.map((item, index) => (
              <li key={index}>
                {item.name} — {item.price} ₽
              </li>
            ))}
          </ul>
        )}
      </div>
    </div>
  
  );
}
