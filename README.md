import { useEffect, useState } from 'react'
import './App.css'

function App() {
  const [items, setItems] = useState([]);
  const [newItem, setNewItem] = useState({ iname: "", amount: "", total: 0 });

  const[billTotal, setBillTotal] = useState(0)
  useEffect(()=>{
    setBillTotal(()=>{

      let data=[...items]

      let temp=0

      for(let i=0;i<data.length;i++){
        temp=parseInt(data[i].total)+temp
      }
      return temp
    })
  },[items])

  const handleChange = (index,e) =>{
    let data=[...items]
    data[index][e.target.name]=e.target.value
    data[index]['total']=(data[index]['amount'])
    setItems(data)
  }

  // Remove
  const removeEntry= (index)=>{
    let data=[...items]
    data.splice(index,1)
    setItems(data)
  }

  const addItem=()=>{
   // const [newItem, setNewItem] = useState([{iname:"", amount:"", total:0}])

   // const newItem = {iname:"", amount:"", total:0}
   // console.log(items);
    // setItem((oldValue)=>{
    //   const newArray=[]

    //   for(let i=0;i<oldValue.length;i++){
    //     newArray.push(oldValue[i])

    //     console.log(oldValue[i]);
    //   }



       
      
     //setNewItem({iname:"", amount:"", total:0})

     

     setItems((oldValue) => [...oldValue, newItem]);

     setNewItem({ iname: "", amount: "", total: 0 });
     // newArray.push(newItem)


     
     if(items[items.length-1].amount===""){
      
      alert("Please enter the amount")
      return;
    }
      return items
    
  }



  const handleSubmit=(e)=>{
    e.preventDefault()
  }

  return (
    <>
      <div className='text-3xl font-bold mb-12 flex justify-center mt-10'>Login</div>
      <div className=' text-xl text-center mb-8 font-bold '>Bill
        <form onSubmit={handleSubmit}>
          <div className="App">
          {newItem.map((input,index)=>(
            <div key={index}>
           <input 
          name='iname'
          value={input.iname}
          placeholder='item name'
          onChange={(e)=> handleChange(index, e)}
           />

          <input name='amount' type="number" placeholder='amount' value={input.amount} onChange={(e)=>handleChange(index,e)}/>
          <input name='total' type="number" placeholder='total' value={input.total} onChange={(e)=>handleChange(index,e)}/>
          <button className='bg-red-600 mb-4' key={index} onClick={()=>removeEntry(index)}>Remove</button>
          </div>
          ))}
          
          
        <button className='border-2 bg-amber-600 mb-8 mt-6 px-2 py-2 ' onClick={addItem}>Add Item</button>
          <h3>Total amount: {billTotal ? billTotal : 0} </h3>
        
          </div>
      </form>
      </div>
    </>
  )
}

export default App
